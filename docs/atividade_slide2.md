# 📑 Projeto de Rede: Centro de Memórias (IFMA)
**IFMA - Campus Itapecuru-Mirim**  
**Disciplina:** Redes de Computadores  
**Alunos:** Igor Cruz, Cauã Pereira e Renato Augusto  

---

## 1. O que é o Projeto? (Explicação Rápida e Simples)
O objetivo deste projeto é planejar e montar a rede de computadores do **Centro de Memórias** utilizando o simulador Cisco Packet Tracer. 

Para que a rede funcione de forma organizada, segura e sem quedas, nós adotamos a **Topologia em Estrela**. Isso significa que todos os computadores do laboratório, a impressora, o servidor e as antenas de Wi-Fi se conectam individualmente a um aparelho centralizador chamado **Switch**. Dessa forma, se um cabo quebrar ou um computador apresentar defeito, apenas aquele aparelho perde a conexão, e todo o resto da rede do Centro continua funcionando normalmente.

---

## 2. Tabela de Equipamentos e Cabos (Sem Complicação)
Para interligar todos os setores da instituição, nós escolhemos os equipamentos e os meios de transmissão pensando no melhor equilíbrio entre custo e desempenho:

| Setor / Conexão | Aparelho Usado | Cabo / Meio Usado | Por que escolhemos isso? (Justificativa) |
| :--- | :--- | :--- | :--- |
| **Internet (Provedor)** | **Modem / ONT** | Cabo Coaxial / Fibra | É o aparelho que recebe o sinal de internet de alta velocidade vindo da rua. |
| **Portão de Saída (Borda)** | Roteador Cisco **2911** | Cabo de Cobre Comum (Cat6) | Serve como a saída obrigatória da nossa rede local para a rede externa (Internet). |
| **Coração da Rede** | Switch Cisco **2960-24TT** | Cabo de Cobre Comum (Cat6) | Conecta todos os aparelhos de forma rápida, inteligente e evita colisões de dados. |
| **Servidor do Mapa** | Servidor Comum | Cabo de Cobre Comum (Cat6) | Precisa ser conectado via cabo diretamente no switch para carregar o mapa de memórias sem lentidão. |
| **Administração** | 1 PC + 1 Impressora | Cabo de Cobre Comum (Cat6) | Ligação via cabo para garantir máxima estabilidade nos serviços administrativos e de impressão. |
| **Laboratório** | 20 Computadores | Cabo de Cobre Comum (Cat6) | Cabos Cat6 para dar alta velocidade (1 Gbps) a baixo custo e de fácil manutenção. |
| **Professores** | Antena Wi-Fi (AP_Professores) | Ondas de Rádio (Wi-Fi 5 GHz) | Fornece sinal sem fio de alto desempenho e menor interferência para os notebooks corporativos. |
| **Visitantes** | Antena Wi-Fi (AP_Visitantes) | Ondas de Rádio (Wi-Fi 2.4 GHz) | Sinal sem fio aberto e de longo alcance para celulares e tablets de quem estiver visitando o local. |

---

## 3. Guia Passo a Passo para Montar no Packet Tracer

### Passo 1: Colocar os Aparelhos na Tela
Clique no menu de equipamentos (canto inferior esquerdo) e arraste para a tela:
1. **Infraestrutura**: 
   * 1 Nuvem (`Cloud-PT`), 1 `Cable Modem` (que representa nossa ONT), 1 Roteador `2911` e 1 Switch `2960-24TT`.
   * 2 Antenas de Wi-Fi (`Access Point-PT`). Renomeie uma para **AP-Professores** e a outra para **AP-Visitantes**.
2. **Computadores e Celulares**:
   * 1 Servidor (renomeado para `Servidor-Mapa`).
   * 1 Computador (`PC-Admin`) e 1 Impressora (`Imp-Admin`).
   * 3 Computadores normais no laboratório (usados para representar as 20 máquinas de forma limpa na tela do trabalho).
   * 2 Laptops (para os Professores) e 2 Celulares (para os Visitantes).

### Passo 2: Trocar a Placa de Rede dos Laptops
Os notebooks no Packet Tracer vêm de fábrica apenas com entrada de cabo. Precisamos colocar uma antena de Wi-Fi neles:
1. Clique no **Laptop** ➔ Vá na aba **Physical** ➔ Clique no **botão de energia** para desligar o aparelho.
2. Arraste a placa de rede com a porta amarela para a gaveta de módulos à esquerda para removê-la.
3. Na lista de módulos, clique em **WPC300N** (módulo Wi-Fi) e arraste-o para o espaço vazio que sobrou no desenho.
4. Clique novamente no **botão de energia** para ligar o Laptop. *(Faça isso nos dois laptops)*.

### Passo 3: Conectar os Cabos do Sistema
Vá no menu de conexões (ícone do **raio**) e selecione o cabo correto para cada ligação:
* **Internet de Borda**: Use o cabo **Coaxial** (linha azul) para ligar a `Cloud` (porta *Coax7*) ao `Cable Modem` (porta *Port0*).
* **Modem ao Roteador**: Use o cabo **Direto de Cobre** (linha preta contínua) para ligar o `Cable Modem` (Port1) ao `Roteador 2911` (GigabitEthernet0/0).
* **Roteador ao Switch**: Use o cabo **Direto de Cobre** (linha preta contínua) para ligar o `Roteador 2911` (GigabitEthernet0/1) ao `Switch 2960` (GigabitEthernet0/1).
* **Equipamentos locais ao Switch** (Todos conectados com o cabo **Direto de Cobre** - linha preta contínua):
  * Conecte o `PC-Admin`, a `Imp-Admin`, o `Servidor-Mapa` e os PCs do Laboratório nas portas de rede (`FastEthernet`) do Switch.
  * Conecte o `AP-Professores` (Port0) e o `AP-Visitantes` (Port0) nas portas restantes do Switch.

### Passo 4: Configurar o Wi-Fi das Antenas
1. **AP-Professores (Wi-Fi Protegido)**:
   * Clique no `AP-Professores` ➔ Acesse a aba **Config** ➔ Selecione **Port 1**.
   * Mude o nome do campo *SSID* para `Professores_IFMA`.
   * Escolha a autenticação **WPA2-PSK** e defina a senha: `senha12345`.
2. **AP-Visitantes (Wi-Fi Aberto)**:
   * Clique no `AP-Visitantes` ➔ Acesse a aba **Config** ➔ Selecione **Port 1**.
   * Mude o nome do campo *SSID* para `Visitantes_IFMA`.
   * Mantenha o campo de autenticação como **Disabled** (rede livre sem senha).

### Passo 5: Conectar Laptops e Celulares no Wi-Fi
* **Laptops (Professores)**: Clique no `Laptop` ➔ Vá na aba **Desktop** ➔ Abra o **PC Wireless** ➔ Vá na aba **Connect** ➔ Selecione a rede `Professores_IFMA` ➔ Clique em **Connect** e insira a senha `senha12345`.
* **Celulares (Visitantes)**: Clique no `SmartPhone` ➔ Vá na aba **Config** ➔ Clique em **Wireless0** ➔ Altere o campo *SSID* para `Visitantes_IFMA`. A conexão sem fio será estabelecida automaticamente.

---

## 4. Endereçamento IP de Teste (Identidade dos Computadores)
Para que os computadores consigam trocar mensagens, precisamos dar um endereço IP de identificação para eles:
* **PC-Admin**: `192.168.1.10`
* **Servidor-Mapa**: `192.168.1.20`
* **PC-Lab-01**: `192.168.1.31`
* **PC-Lab-02**: `192.168.1.32`

---

## 5. Por que aparecem Cartinhas com um "X" Vermelho na Simulação?
Quando nós abrimos o **Command Prompt** (Prompt de Comando) do *PC-Lab-01* e testamos a comunicação digitando o comando `ping 192.168.1.20` (IP do Servidor), o simulador mostra várias cartinhas com um **"X" vermelho**. 

**Isso é um comportamento normal e indica que a rede está perfeita!**

### Como isso funciona de forma simples:
1. **A Pergunta Geral (Broadcast):** O computador do aluno precisa falar com o Servidor, mas ainda não sabe o endereço físico (MAC Address) dele. Por isso, ele envia uma mensagem geral para a rede perguntando: *"Quem aqui tem o IP do Servidor?"*
2. **A Distribuição pelo Switch:** O Switch recebe essa pergunta e envia uma cópia para **todos** os aparelhos que estão ligados nas suas portas.
3. **O Descarte Saudável (O "X"):** Os outros computadores, a impressora e as antenas de Wi-Fi recebem a carta, abrem e leem a pergunta. Ao perceberem que o IP de destino não é o deles, eles rejeitam a mensagem e a jogam no lixo. **No simulador, esse descarte de segurança é representado pelo "X" vermelho**.
4. **A Resposta do Destinatário:** Apenas o Servidor reconhece que a mensagem é para ele, responde diretamente de volta para o computador do aluno, e a conexão se estabelece sem mais nenhum descarte.

---

## 6. Roteiro para Explicar ao seu Professor (Apresentação Rápida)
Se o seu professor pedir para você explicar o seu projeto, leia ou fale estes 3 pontos simples:

1. *"Professor, o nosso grupo (Igor, Cauã e Renato) montou a rede do Centro de Memórias em **Topologia em Estrela**. Todos os setores se conectam de forma individual ao Switch central, o que evita que uma falha em um computador derrube a rede dos outros."*
2. *"Nós planejamos os meios de transmissão com foco nas necessidades: usamos cabos de cobre para dar velocidade máxima e estabilidade ao laboratório e à administração, e usamos antenas de Wi-Fi separadas para trazer mobilidade aos professores e acesso fácil para os visitantes."*
3. *"Na simulação, as cartinhas com 'X' vermelho representam o **descarte de pacotes ARP**. Isso prova que o protocolo de segurança está ativo: os computadores que não são o destino da mensagem descartam os pacotes de forma saudável, enquanto apenas o servidor responde diretamente para estabelecer o teste de Ping."*