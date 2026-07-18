# RELATÓRIO DE AULA PRÁTICA: MODELOS OSI E TCP/IP

**Instituição:** Instituto Federal de Educação, Ciência e Tecnologia do Maranhão (IFMA) - Campus Itapecuru-Mirim  
**Turma:** info-200  
**Professor:** Professor Thales Valente  
**Alunos:** Igor Cruz, Cauã Pereira e Renato Augusto  
**Data da Aula:** 16 de Julho de 2026  
**Referência:** Dia 2 - Aula 4 (Modelos OSI e TCP/IP) | Slides 1 a 37  

---

## 1. O que raios é um "Modelo" e uma "Camada"?

Para entender como a rede funciona por dentro, o professor Thales explicou que a gente precisa de um **Mapa**. Uma rede de computadores é um sistema muito complexo, e tentar entender tudo de uma vez dá um nó na cabeça.

*   **O Modelo:** É como um mapa de uma cidade. Ele não é a cidade real, mas ajuda você a andar por ela sem se perder. No nosso caso, o modelo divide as responsabilidades da rede em pedaços menores.
*   **A Camada:** Cada camada cuida de um problema específico. O mais legal é que uma camada resolve o seu problema, passa o resultado para a camada de cima e não precisa ficar explicando "como" fez o trabalho. É pura divisão de tarefas!
*   **Serviço vs. Protocolo:** O **Serviço** diz *o que* a camada faz (ex: "vou entregar um arquivo"). O **Protocolo** são as regras de *como* ela faz isso (ex: "vamos dividir esse arquivo em 4 partes e mandar uma por uma").

---

## 2. Modelo OSI (O Mapa Teórico) vs. Modelo TCP/IP (A Internet de Verdade)

Existem duas formas principais de desenhar esse mapa de camadas:

```text
  [ MODELO OSI ]             [ MODELO TCP/IP ]         [ MODELO HÍBRIDO ]
  (7 Camadas - Teórico)      (4 Camadas - Prático)     (5 Camadas - Didático)
  
  +-------------------+       +-----------------+       +-----------------+
  | 7. Aplicação      |------>|                 |       | 5. Aplicação    |
  | 6. Apresentação   |------>| 4. Aplicação    |------>|                 |
  | 5. Sessão         |------>|                 |       |                 |
  +-------------------+       +-----------------+       +-----------------+
  | 4. Transporte     |------>| 3. Transporte   |------>| 4. Transporte   |
  +-------------------+       +-----------------+       +-----------------+
  | 3. Rede           |------>| 2. Internet     |------>| 3. Rede         |
  +-------------------+       +-----------------+       +-----------------+
  | 2. Enlace         |------>|                 |       | 2. Enlace       |
  +-------------------+       | 1. Acesso à Rede|------>+-----------------+
  | 1. Física         |------>|                 |       | 1. Física       |
  +-------------------+       +-----------------+       +-----------------+
```

*   **Modelo OSI:** Tem 7 camadas. Ele é o padrão universal para estudar, mas na prática, nenhum computador usa ele tintim por tintim. É mais para referência de engenheiros.
*   **Modelo TCP/IP:** Tem 4 camadas (segundo a RFC 1122). É o modelo que o seu computador, o seu celular e toda a Internet usam de verdade. Ele junta as funções de software em menos camadas para ser mais rápido e eficiente.
*   **Modelo Híbrido:** Tem 5 camadas. É o que a gente mais vê nos livros de faculdade e escola técnica porque separa a parte física do cabo (Física) das regras da placa de rede local (Enlace), facilitando nossa vida na hora de estudar.

---

## 3. O que é PDU e a analogia das Bonecas Russas (Encapsulamento)

Quando você clica em um link para abrir uma página web (`http://192.168.10.100`), o seu navegador gera um bloco de dados. Esse dado precisa viajar pelo cabo, mas ele não vai "puro".

Aí entra a **PDU (Protocol Data Unit)**, que é o nome chique para o "envelope" de cada camada. O processo de envio se chama **Encapsulamento**, e funciona igualzinho àquelas bonecas russas (Matryoshka), onde uma caixa vai dentro da outra:

1.  **Camadas 7, 6, 5 (Aplicação):** O dado puro é gerado (ex: uma requisição HTTP pedindo a página). A PDU aqui chama simplesmente **Dados** ou **Mensagem**.
2.  **Camada 4 (Transporte):** Os dados ganham um cabeçalho com as **Portas Lógicas** (origem e destino). Se o dado for gigante, ele é cortado em pedaços. A PDU aqui chama **Segmento**.
3.  **Camada 3 (Rede):** O segmento entra dentro de outra caixa e ganha os **Endereços IP** de origem e destino. A PDU aqui ganha o nome de **Pacote**.
4.  **Camada 2 (Enlace):** O pacote entra em mais um envelope, ganhando os **Endereços MAC** físicos e um detector de erros no final (Trailer FCS). A PDU aqui chama **Quadro (ou Frame)**.
5.  **Camada 1 (Física):** O quadro vira energia pura! São os **Bits** (0 e 1) transmitidos por eletricidade no cabo de cobre, luz na fibra óptica ou ondas no Wi-Fi.

Quando o dado chega no servidor de destino, acontece o **Desencapsulamento**: o servidor vai abrindo caixa por caixa, lendo as etiquetas de trás para frente, até sobrar só o dado puro que o usuário pediu.

---

## 4. Quem lê o quê? (Switch vs. Roteador)

Uma das maiores pegadinhas em redes é achar que todo equipamento lê o pacote inteiro. Não lê!

*   **O Switch trabalha na Camada 2 (Enlace):** Ele é meio cego para o resto das coisas. Ele só abre a caixinha do Quadro para ler os endereços MAC de origem e destino e ver se o arquivo não veio corrompido (FCS). Ele ignora o IP, ignora as portas e não faz ideia se você está acessando o site do IFMA ou jogando online.
*   **O Roteador trabalha na Camada 3 (Rede):** Ele vai um pouco mais fundo. Quando o quadro chega nele, ele arranca o cabeçalho MAC fora (desencapsula), abre a caixa da Camada 3 e lê o **Endereço IP de Destino** para descobrir qual o melhor caminho para mandar os dados na Internet. Depois, ele embrulha o pacote em um **novo quadro com novos MACs** (reencapsula) e joga no cabo de novo. 
*   *Regra de ouro:* O endereço IP nunca muda do início ao fim da jornada, mas o endereço MAC muda a cada equipamento de rede (salto) que o pacote atravessa!

---

## 5. Resumo Curto (Para Fixar na Mente)

*   **Modelos e Camadas:** Servem para dividir o trabalho da rede. Cada camada faz sua função e joga para cima.
*   **Nomes das PDUs:** Dados (Aplicação) -> Segmento (Transporte) -> Pacote (Rede) -> Quadro (Enlace) -> Bits (Física). Errar esses nomes em uma conversa técnica passa vergonha!
*   **Encapsulamento:** Colocar caixas dentro de caixas, adicionando cabeçalhos com instruções de entrega.
*   **Dispositivos:** Switch só enxerga o MAC (Camada 2). Roteador enxerga o IP (Camada 3) e decide a rota.