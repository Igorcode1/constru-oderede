# RELATÓRIO DE ATIVIDADE PRÁTICA: O PRIMEIRO PING E O MISTÉRIO DO ARP

**Instituição:** Instituto Federal de Educação, Ciência e Tecnologia do Maranhão (IFMA) - Campus Itapecuru-Mirim  
**Turma:** info-200  
**Professor:** Professor Thales Valente  
**Alunos:** Igor Cruz, Cauã Pereira e Renato Augusto  
**Data:** 17 de Julho de 2026  
**Referência:** Dia 2 - Aula 3 (Ethernet, MAC, Switches e ARP) | Slide 5, Página 37  

---

## 1. Como ficou montada a nossa rede?

O cenário é bem simples: ligamos dois computadores em um Switch usando cabos de rede normais (par trançado direto). Como eles estão na mesma vizinhança (sub-rede local), não precisamos de roteador nem de gateway. É papo direto de PC para PC!

```text
       +-------------------------------------------------------+
       |                  REDE LOCAL (LAN)                     |
       |               Sub-rede: 192.168.10.0/24               |
       +-------------------------------------------------------+
                                   |
         [ PC0 ]                   |                   [ PC1 ]
  IP: 192.168.10.10                |            IP: 192.168.10.20
  Plugado na porta: Fa0/1          |            Plugado na porta: Fa0/2
           |                       |                       |
           +--------------------->| |<--------------------+
                               | SWITCH |
                               +--------+
```

---

## 2. O que a gente fez na prática?

Para conseguir olhar as "cartinhas" (pacotes) viajando por dentro do cabo, nós seguimos esses passos no simulador:

1.  **Montamos o esqueleto:** Colocamos os dois PCs e o Switch na tela e conectamos os cabos nas placas FastEthernet.
2.  **Ligamos o "Raio-X":** Mudamos o Packet Tracer do modo normal para o **Modo Simulação**. Fomos nos filtros e limpamos aquela bagunça de protocolos, deixando ativados apenas o **ARP** e o **ICMP** (que é o protocolo do famoso Ping).
3.  **Soltamos o comando:** Abrimos o terminal do `PC0` e mandamos um:
    ```bash
    ping 192.168.10.20
    ```
4.  **Espiamos os envelopes:** Clicamos nos envelopes coloridos que apareceram na tela e fomos direto na aba **In Layers / Out Layers**, olhando a **Camada 2** para descobrir quais endereços MAC estavam carimbados ali dentro.

---

## 3. Comandos que usamos para bisbilhotar a memória

Depois que o teste terminou e os PCs terminaram de conversar, rodamos dois comandos para ver o que eles tinham aprendido e guardado na memória RAM:

*   **No PC0 (`arp -a`):** Mostra o "Cache ARP". É uma tabelinha que o computador cria para não ter que ficar perguntando toda hora quem é quem. Ela basicamente diz: *"O IP 192.168.10.20 pertence à placa física com o MAC tal"*.
*   **No Switch (`show mac-address-table`):** Mostra a famosa Tabela CAM. O Switch guarda nela uma lista de "quem está em qual tomada". Ele anota que na porta física `Fa0/1` está o MAC do `PC0` e na `Fa0/2` está o MAC do `PC1`.

---

## 4. A Dança dos Pacotes: Como funciona o fluxo invisível da rede?

O professor Thales explicou que quando você dá o primeiro ping em uma rede que acabou de ser ligada, acontece uma saga invisível nos cabos antes do comando dar sucesso:

1.  **O PC0 fica travado:** O `PC0` quer mandar o Ping (ICMP) para o `PC1`. Ele sabe o IP do destino, mas para jogar o dado no cabo físico, ele precisa do endereço da placa de rede (o MAC). Como o cache dele está totalmente vazio, o pacote de Ping fica congelado na fila de espera.
2.  **O Grito de Socorro (ARP Request):** Para resolver isso, o `PC0` cria um pacote chamado **ARP Request**. É basicamente um grito na rede: *"Ei galera, quem aí tem o IP 192.168.10.20? Me passa seu MAC!"*. Como ele não sabe para quem enviar, ele carimba o destino como **Broadcast** (`FF:FF:FF:FF:FF:FF`), que significa "para todo mundo ouvir".
3.  **O Switch aprende e espalha:** Quando o grito entra pela porta `Fa0/1`, o Switch lê o MAC de origem do `PC0` e já anota na tabela dele: *"O PC0 está na Fa0/1"*. Como a mensagem é para todo mundo (Broadcast), o Switch faz um *Flooding* (inunda a rede) e joga uma cópia dessa mensagem para todas as outras portas ativas.
4.  **A Resposta Direta (ARP Reply):** O `PC1` recebe a mensagem. Ele olha o IP e diz: *"Opa, sou eu!"*. Os outros computadores da rede ignoram, mas o `PC1` cria um **ARP Reply** dizendo: *"Meu IP é esse e meu MAC é X"*. Essa resposta vai em **Unicast** (direto para o MAC do `PC0`), porque o `PC1` já aprendeu o endereço do `PC0`.
5.  **O Switch anota de novo:** O Switch intercepta a resposta vindo da porta `Fa0/2`, anota na tabela que o `PC1` está ali, e entrega o pacote direto na mão do `PC0`, sem mandar para mais ninguém.
6.  **O Ping finalmente é liberado!:** Agora que o `PC0` salvou o MAC do `PC1` na tabela ARP dele, o pacote do Ping original é descongelado. Ele monta o quadro com o MAC certo e envia. Como o Switch já sabe a tabela de cor, o Ping vai direto e reto pro destino, e a resposta volta sem gerar tráfego desnecessário!

---

## 5. Resumo Curto (Para Fixar na Mente)

*   **O Problema:** O computador sabe o endereço lógico (IP), mas a rede local precisa do endereço físico (MAC) para entregar o dado no cabo.
*   **O Salvador (ARP):** O protocolo ARP faz o meio de campo, descobrindo o endereço MAC a partir de um IP conhecido.
*   **Broadcast vs Unicast:** O pedido do ARP vai para todo mundo ouvir (`FF:FF...`), mas a resposta volta direto (Unicast) para quem perguntou.
*   **O Switch é inteligente:** Ele monta sua tabela de portas e MACs sozinho, apenas olhando quem está enviando mensagens na rede.