# 📑 Projeto de Rede: Centro de Memórias (IFMA)

**IFMA - Campus Itapecuru-Mirim**  
**Disciplina:** Redes de Computadores  
**Alunos:** Igor Cruz, Cauã Pereira e Renato Augusto  

---

## 1. Visão Geral e Topologia (O Desenho da Rede)

Para garantir que a rede do Centro de Memórias funcione de forma organizada, estável e sem quedas gerais, adotamos a **Topologia em Estrela**. 

Nesse modelo, todos os dispositivos (computadores, impressoras, servidores e antenas Wi-Fi) conectam-se individualmente a um aparelho centralizador chamando **Switch**. Se um cabo romper ou um computador falhar, apenas aquele ponto perde o sinal; todo o restante da instituição continua operando normalmente.

```text
  [Mundo Externo]   ➔   [Provedor]    ➔   [Portão de Entrada]
   Nuvem (Internet)     Modem (ONT)       Roteador Cisco 2911
                                                  │
                                                  ▼
                                        [ O CORAÇÃO DA REDE ]
                                         Switch Cisco 2960
                                                  │
         ┌──────────────────────┬─────────────────┴────────┬──────────────────────┐
         ▼                      ▼                          ▼                      ▼
  [Setor de Dados]       [Administração]            [Laboratório]           [Redes Wi-Fi]
   Servidor do Mapa       1 PC + 1 Impressora        20 Computadores         • AP Professores (Fechado)
                                                                             • AP Visitantes (Aberto)
```

---

## 2. Tabela Enxuta de Equipamentos

Os equipamentos e conexões foram selecionados para oferecer o melhor equilíbrio entre custo, desempenho e facilidade de manutenção:

| Equipamento | Setor / Função Direta | Conexão / Meio Usado | Justificativa Simples |
| :--- | :--- | :--- | :--- |
| **Modem / ONT** | Internet (Provedor) | Cabo Coaxial / Fibra | Recebe o sinal de internet de alta velocidade da rua. |
| **Roteador Cisco 2911** | Borda (Saída da Rede) | Cabo de Cobre (Cat6) | Funciona como o portão de saída obrigatório da rede local para a Internet. |
| **Switch Cisco 2960** | Coração da Rede | Cabo de Cobre (Cat6) | Interliga todos os aparelhos de forma inteligente e sem colisões. |
| **Servidor Comum** | Servidor do Mapa | Cabo de Cobre (Cat6) | Ligação direta via cabo para carregar o mapa de memórias sem lentidão. |
| **Computadores / Impressora**| Laboratório e Admin | Cabo de Cobre (Cat6) | Cabos Cat6 garantem velocidade estável de 1 Gbps a baixo custo. |
| **AP_Professores** | Wi-Fi Docentes | Ondas de Rádio (5 GHz) | Sinal de alto desempenho e menor interferência (Protegido por senha). |
| **AP_Visitantes** | Wi-Fi Público | Ondas de Rádio (2.4 GHz)| Sinal aberto de longo alcance para celulares e tablets de visitantes. |

---

## 3. Conceito Chave: O Mistério das "Cartinhas com X"

Ao rodar a simulação no Cisco Packet Tracer e testar a comunicação usando o comando `ping` a partir de um computador do laboratório, é normal ver envelopes com um **"X" vermelho** aparecendo na tela. 

**Isso prova que a rede está configurada perfeitamente e funcionando de forma segura!**

* **A Pergunta Geral (Broadcast):** O computador de origem precisa falar com o Servidor, mas ainda não conhece o endereço físico dele (MAC Address). Ele envia uma pergunta para a rede inteira: *"Quem tem o IP do Servidor?"*
* **O Repasse do Switch:** O Switch duplica essa pergunta e a entrega para todas as portas ativas.
* **O Descarte Saudável (O "X"):** Os computadores da administração, as impressoras e as antenas Wi-Fi leem a pergunta e percebem que o IP de destino não é deles. Por segurança, eles rejeitam e descartam o pacote. **No simulador, esse descarte é o "X" vermelho.**
* **A Resposta:** Apenas o Servidor real aceita a mensagem, responde de volta diretamente para o computador do aluno e a conexão se estabelece.

---

## 4. Roteiro de Apresentação (30 Segundos por Aluno)

Se o professor pedir para o grupo explicar o projeto rapidamente na bancada, usem esta divisão direta:

* **Aluno 1 (O Conceito):** *"Professor, nosso grupo estruturou a rede do Centro de Memórias usando a **Topologia em Estrela**. Escolhemos esse modelo porque centraliza a comunicação no Switch. Isso traz segurança, pois se um computador do laboratório ou da recepção quebrar, a falha fica isolada e o resto do IFMA continua funcionando."*
* **Aluno 2 (A Prática):** *"Para os meios de transmissão, priorizamos cabos de cobre Cat6 para os computadores e o servidor, garantindo uma taxa de transmissão estável de 1 Gbps. Para a rede sem fio, separamos em duas antenas: uma de 5 GHz protegida por senha para os notebooks dos professores e outra de 2.4 GHz aberta para os visitantes."*
* **Aluno 3 (A Simulação):** *"No Packet Tracer, validamos a rede com o teste de ping. Aquelas cartinhas com 'X' vermelho que aparecem no simulador são os descartes normais do protocolo ARP. Elas provam que os computadores vizinhos estão rejeitando pacotes que não pertencem a eles, confirmando que a lógica de segurança e o endereçamento IP estão funcionando perfeitamente."*