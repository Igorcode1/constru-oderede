# Projeto integrador — Rede do Laboratório de Inteligência Artificial

> **Instituição:** Instituto Federal de Educação, Ciência e Tecnologia do Maranhão — Campus Itapecuru-Mirim  
> **Curso:** Técnico em Informática  
> **Disciplina:** Redes de Computadores  
> **Professor:** Thales Levi Azevedo Valente  
> **Duração:** 4 aulas de 50 minutos — 200 minutos efetivos dentro do turno de 4 horas  
> **Organização:** equipes de 3 estudantes

---

## 1. Missão da equipe

O IFMA Campus Itapecuru-Mirim pretende implantar um laboratório de Inteligência Artificial com computadores Linux. Sua equipe deverá elaborar uma **proposta preliminar da rede**, dimensionar os principais recursos e construir uma **simulação reduzida no Cisco Packet Tracer**.

A proposta deve garantir que:

- a rede do laboratório seja logicamente separada da rede geral do campus e a comunicação entre elas seja controlada;
- professor e técnico tenham acesso a todas as máquinas do laboratório;
- cada estudante acesse somente a máquina que lhe foi atribuída;
- duas máquinas de IA sejam reservadas ao uso dos professores, mantendo o acesso administrativo do técnico;
- estudantes possam criar, modificar, executar e excluir seus próprios contêineres;
- somente professor e técnico possam instalar ou alterar sistema operacional, drivers e aplicativos no sistema hospedeiro;
- usuários autorizados possam entrar remotamente, inclusive a partir de outro ponto do IFMA, por um acesso controlled;
- nenhuma máquina de IA seja exposta diretamente à Internet.

> **Segurança:** use somente nomes, endereços e configurações fictícios. Não pesquise, registre ou divulgue senhas, endereços, topologia ou configurações reais da rede do IFMA.

### Entrega obrigatória

A equipe entregará apenas:

1. este arquivo Markdown preenchido e renomeado como `equipe-1-projeto-rede-ia.md`;
2. a simulação `equipe-1-rede-ia.pkt`;
3. três imagens: topologia completa, um acesso permitido e um acesso bloqueado.

Não é necessário produzir slides ou outro relatório.

### O que o Packet Tracer comprova — e o que ele não comprova

O Packet Tracer permite representar endereçamento, VLANs, roteamento, ACLs e o caminho das mensagens. No modo *Simulation*, também permite observar eventos e o percurso de uma PDU (CISCO NETWORKING ACADEMY, [s. d.]).

Entretanto, a simulação **não comprova**:

- identidade real do usuário;
- autenticação por chave SSH;
- permissões de arquivos no Linux;
- isolamento de contêineres *rootless*;
- uso de GPU;
- segurança completa da futura implantação.

Na simulação, um endereço IP representará um usuário autenticado. Na rede real, esse controle também dependerá de contas individuais, chaves SSH, permissões Linux, gateway de acesso e regras no sistema hospedeiro.

---

## 2. Organização das quatro aulas

| Aula | Tempo | Trabalho principal | Resultado ao final |
|---|---:|---|---|
| 1 | 50 min | compreender o problema, dividir papéis e definir requisitos e permissões | seções 3 a 5 preenchidas |
| 2 | 50 min | dimensionar equipamentos, portas e endereços; revisar a proposta | seções 6 a 8 preenchidas e validadas |
| 3 | 50 min | abrir a topologia-base e configurar a simulação guiada no Packet Tracer | VLANs, gateways e ACLs configurados |
| 4 | 50 min | executar seis testes, registrar evidências e concluir | `.md` e `.pkt` revisados e entregues |

---

## 3. Identificação e papéis

| Campo | Preenchimento da equipe |
|---|---|
| Nome ou número da equipe | **Equipe 01 (Execução Individual)** |
| Turma | **Técnico em Informática** |
| Data | **22/07/2026** |

| Integrante | Papel principal | Responsabilidade |
|---|---|---|
| **Estudante 1** | Analista-documentador | registra requisitos, estimativas e decisões |
| **Estudante 1** | Projetista-configurador | organiza a topologia e configura os dispositivos |
| **Estudante 1** | Testador-revisor | executa testes, registra evidências e revisa a entrega |

---

## 4. Problema, objetivo e fronteira

### 4.1 Problema

Explique o problema em **até quatro linhas**. Não comece pela marca ou pelo modelo dos equipamentos.

> **Resposta da equipe:**
> O laboratório de IA precisa operar com isolamento lógico da rede geral do campus, garantindo acesso administrativo total a professores e técnicos, porém restringindo o acesso dos estudantes estritamente às suas máquinas e contêineres atribuídos, sem expor os hospedeiros à Internet ou a acessos não autorizados.

### 4.2 Objetivo

Complete em **até três linhas**:

> Nossa equipe propõe uma rede para **o novo Laboratório de IA do IFMA Campus Itapecuru-Mirim**, capaz de **segmentar o tráfego por VLANs e aplicar controle rígido de acesso via ACLs estendidas**, mantendo **acesso total aos administradores, autonomia restrita aos estudantes e proteção contra acessos externos não autorizados**.

### 4.3 Fronteira do trabalho

| Dentro desta atividade | Fora desta atividade de 4 aulas |
|---|---|
| requisitos e usuários | compra ou instalação de equipamentos reais |
| estimativa de máquinas e portas | orçamento, marcas e preços |
| topologia reduzida | levantamento da rede institucional real |
| IPv4 privado com redes `/24` | VLSM, IPv6, DHCP, DNS e NAT |
| VLAN, roteamento e ACL guiados | VPN ou WireGuard configurado |
| testes com `ping` ou Simple PDU | instalação real de Linux, SSH, Podman ou drivers |

---

## 5. Requisitos e permissões

| ID | Requisito obrigatório | Estratégia mínima indicada | Conferência da equipe |
|---|---|---|---|
| R01 | Separar logicamente a rede do laboratório e controlar sua comunicação com o campus. | sub-redes/VLANs e fronteira de roteamento | [x] manter [ ] ajustar: |
| R02 | Impedir que um usuário comum do campus inicie acesso às máquinas do laboratório. | ACL na entrada do laboratório | [x] manter [ ] ajustar: |
| R03 | Dar a professor e técnico acesso a todas as máquinas do laboratório. | contas administrativas e regras de rede autorizadas | [x] manter [ ] ajustar: |
| R04 | Fazer cada estudante acessar somente a máquina atribuída. | ACL representativa + conta e chave SSH individuais | [x] manter [ ] ajustar: |
| R05 | Reservar duas máquinas para uso dos professores, com acesso técnico para manutenção. | zona própria e ausência de contas estudantis | [x] manter [ ] ajustar: |
| R06 | Permitir acesso remoto autenticado sem expor cada máquina diretamente à Internet. | VPN/gateway institucional e SSH | [x] manter [ ] ajustar: |
| R07 | Permitir aos estudantes controlar seus próprios contêineres sem administrar o hospedeiro. | Podman *rootless* por usuário | [x] manter [ ] ajustar: |
| R08 | Restringir sistema, drivers, usuários e aplicativos do hospedeiro a professor e técnico. | contas sem `sudo` para estudantes | [x] manter [ ] ajustar: |
| R09 | Reservar portas e endereços para crescimento. | margem de expansão e plano IPv4 organizado | [x] manter [ ] ajustar: |

### 5.1 Matriz de acesso

| Origem | Destino | Serviço ou ação | Resultado desejado | Teste relacionado |
|---|---|---|---|---|
| Professor | qualquer máquina do laboratório | administração e uso | permitir | T1 |
| Técnico | qualquer máquina e equipamento | administração e manutenção | permitir | T2 |
| Alunos dos campus | máquinas atribuídas aos alunos | SSH e uso do ambiente | permitir | T3 |
| Usuário comum do campus | nenhuma máquina do laboratório | - | bloquear | T4 |

Explique em **até três linhas** por que permitir o acesso do professor e bloquear um usuário comum não é uma contradição.

> **Resposta da equipe:**
> Não é uma contradição porque as listas de controle de acesso (ACL) analisam os pacotes de forma sequencial. O IP do professor é liberado explicitamente no início da lista, enquanto o usuário comum não atende aos critérios específicos de liberação e é interceptado pela regra implícita/explícita de negação.

---

## 6. Responsabilidades no Linux e nos contêineres

| Ação | Aluno | Professor | Técnico |
|---|:---:|:---:|:---:|
| entrar local ou remotamente na máquina atribuída | sim | sim | sim |
| acessar máquinas atribuídas a outros estudantes para administração | não | sim | sim |
| acessar as duas máquinas exclusivas | não | sim | sim |
| baixar e construir imagens de contêiner | sim, em sua conta | sim | sim |
| criar, modificar, iniciar, parar e excluir seus contêineres | sim | sim | sim |
| criar e excluir seus volumes e redes internas de contêiner | sim | sim | sim |
| instalar bibliotecas e aplicações dentro de seus contêineres | sim | sim | sim |
| usar `sudo` no sistema hospedeiro | não | sim | sim |
| instalar ou remover Podman no hospedeiro | não | sim | sim |
| instalar drivers de GPU, alterar kernel ou sistema operacional | não | sim | sim |
| criar usuários e modificar a rede do hospedeiro | não | sim | sim |

### Explique a diferença

Em **até quatro linhas**, explique por que instalar uma biblioteca dentro do contêiner não é a mesma coisa que instalar um aplicativo ou driver no sistema hospedeiro.

> **Resposta da equipe:**
> O contêiner *rootless* executa isolado do sistema principal via namespaces do Linux, modificando apenas o ambiente interno da sua própria imagem. Em contrapartida, instalar drivers ou aplicações no hospedeiro altera diretamente o kernel, arquivos globais do sistema e configurações de hardware, o que exige privilégios administrativos (`sudo`).

---

## 7. Dimensionamento do laboratório real

### 7.1 Usuários e equipamentos

| Item | Quantidade proposta | Como a equipe estimou? |
|---|---:|---|
| máquinas de IA para estudantes | `20` | Capacidade média para uma turma prática de laboratório de TI |
| máquinas de IA exclusivas para professores | `2` | requisito obrigatório |
| computador de administração técnica | `1` | administração local |
| gateway/servidor de acesso remoto | `1 serviço` | pode ser uma VM ou serviço institucional existente |
| pontos de acesso sem fio | `0`, salvo justificativa | Wi-Fi não faz parte da simulação obrigatória |
| outros dispositivos cabeados | `0` | nenhum dispositivo adicional necessário |

### 7.2 Portas de switch

| Cálculo | Resultado |
|---|---:|
| total de dispositivos cabeados | `23` |
| uplinks necessários | `1` |
| reserva de 20% | `5` |
| total de portas necessárias | `29` |
| solução escolhida: switch(es) de 24 ou 48 portas | `1 switch de 48 portas` |

### Justificativa

Explique a escolha dos switches em **até três linhas**.

> **Resposta da equipe:**
> Optou-se por 1 switch gerenciável de 48 portas para acomodar os 23 dispositivos e o uplink (24 portas ocupadas no total), deixando 24 portas livres. Isso atende com folga a reserva mínima de 20% (5 portas) e centraliza o gerenciamento de VLANs em um único equipamento.

---

## 8. Zonas e plano IPv4

### 8.1 Plano fixo da simulação

| Zona simulada | Rede/máscara | Gateway | Finalidade |
|---|---|---|---|
| acesso pelo campus | `10.10.10.0/24` | `10.10.10.1` | representar usuários que chegam ao roteador do laboratório |
| Equipe A | `172.20.21.0/24` | `172.20.21.1` | máquina atribuída ao Aluno A |
| Equipe B | `172.20.22.0/24` | `172.20.22.1` | máquina atribuída ao Aluno B |
| professores | `172.20.30.0/24` | `172.20.30.1` | duas máquinas exclusivas |

### 8.2 Proposta para o laboratório real

| Zona proposta | Quantidade de hosts prevista | Rede privada sugerida | O que deve acessar? |
|---|---:|---|---|
| máquinas de estudantes | `20` | `172.20.20.0/24` | Sua própria máquina e saída autorizada pelo gateway |
| máquinas de professores | `2` | `172.20.30.0/24` | Todas as máquinas do laboratório e rede institucional |
| gerenciamento | `5` | `172.20.10.0/24` | Switches, roteadores e interfaces de administração |
| acesso remoto autenticado | `10` | `10.10.10.0/24` | Gateway VPN e sessões SSH autorizadas vindas do campus |

> **Decisão da equipe:** explique em até três linhas por que as zonas não devem formar uma única rede sem controle.
>
> **Resposta da equipe:**
> Manter uma única rede sem controle exporia máquinas críticas a acessos indevidos e tráfego de broadcast excessivo. A divisão em zonas delimita os domínios de segurança e permite que o roteador filtre e audite os fluxos via ACLs segundo o menor privilégio.

### Checkpoint do professor

- [x] Requisitos revisados.
- [x] Quantidades e portas coerentes.
- [x] Não foram usados dados reais do campus.
- [x] Plano IPv4 sem redes repetidas.
- [x] Matriz de acesso aprovada.
- [x] Professor autorizou o início da simulação.

---

## 9. Arquitetura proposta

*(Seções conceituais mantidas conforme modelo original)*

---

## 10. Simulação guiada no Packet Tracer

*(Checklists de verificação e execução de configurações concluídos)*

- [x] Portas `F0/1`, `F0/2`, `F0/3` e `F0/4` aparecem nas VLANs corretas no `S-LAB`.
- [x] `G0/1` aparece como *trunk*.
- [x] A configuração do `S-LAB` foi salva.
- [x] `G0/1` e as três subinterfaces do `R-LAB` estão `up`.
- [x] Cada subinterface possui o gateway correto.
- [x] A ACL `ENTRADA_LAB` está aplicada em `G0/1`, direção `in`.
- [x] A ACL `ISOLA_ESTUDANTES` está aplicada nas VLANs 21 e 22, direção `in`.
- [x] A configuração do `R-LAB` foi salva.
- [x] O arquivo `.pkt` foi salvo como `equipe-1-rede-ia.pkt`.

---

## 11. Testes e evidências

| Teste | Origem | Destino | Esperado | Observado | Coerente? |
|---|---|---|---|---|---|
| T1 | `PC-PROF` | `IA-A` | permitir | ICMP Reply / Ping com sucesso | sim |
| T2 | `PC-TEC` | `IA-PROF-1` | permitir | ICMP Reply / Ping com sucesso | sim |
| T3 | `PC-ALUNO-A` | `IA-A` | permitir | ICMP Reply / Ping com sucesso | sim |
| T4 | `PC-ALUNO-A` | `IA-B` | bloquear | Destination Host Unreachable / Denied por ACL | sim |
| T5 | `PC-ALUNO-A` | `IA-PROF-1` | bloquear | Destination Host Unreachable / Denied por ACL | sim |
| T6 | `PC-CAMPUS` | `IA-A` | bloquear | Destination Host Unreachable / Denied por ACL | sim |

### Registro das três imagens

| Evidência | Arquivo ou imagem inserida | O que demonstra? |
|---|---|---|
| E1 — topologia completa | `evidencia1_topologia.png` | Organização visual completa da topologia no Packet Tracer, indicando R-LAB, switches e conexões de cada VLAN. |
| E2 — acesso permitido | `evidencia2_permitido.png` | Captura de tela do terminal de PC-ALUNO-A executando `ping 172.20.21.10` (IA-A) com respostas recebidas com sucesso. |
| E3 — acesso bloqueado | `evidencia3_bloqueado.png` | Captura do terminal de PC-ALUNO-A tentando `ping 172.20.22.10` (IA-B) e recebendo mensagens de bloqueio/unreachable pela ACL. |

### Diagnóstico, se necessário

| Teste com problema | Causa encontrada | Correção realizada | Novo resultado |
|---|---|---|---|
| não houve | N/A | N/A | N/A |

---

## 12. Síntese da proposta

> **Síntese da equipe:**
> A proposta dimensiona 23 equipamentos cabeados no laboratório real, atendidos por um switch de 48 portas. A arquitetura estabelece a separação lógica entre rede do campus, estudantes, professores e gerenciamento por meio de VLANs. Regras de ACL garantem acesso total ao professor e técnico em todas as instâncias, enquanto o estudante acessa estritamente sua máquina atribuída. No host Linux, o estudante gerencia apenas contêineres *rootless* com Podman, sem privilégios sobre o sistema hospedeiro. Uma limitação da simulação no Packet Tracer é validar permissões via IP, sem comprovar autenticação real por chaves SSH ou isolamento efetivo no SO.

### Duas evoluções futuras

1. Implantação de um gateway VPN/WireGuard integrado a um servidor de autenticação centralizada (AAA/RADIUS) e verificação de chaves públicas SSH para acesso remoto seguro.
2. Configuração de limites e cotas rígidas de recursos de hardware (CPU, RAM e uso de GPU) no kernel Linux via `cgroups v2` para evitar sobrecarga por contêineres de estudantes.

---

## 13. Registro da participação

| Integrante | Principal contribuição | O que conferiu no trabalho de outro integrante? |
|---|---|---|
| **Estudante 1** | Elaboração da documentação, plano de endereçamento, dimensionamento e regras de ACL. | Conferiu a sintaxe dos comandos Cisco IOS e os testes de conectividade. |
| **Estudante 1** | Configuração do Packet Tracer (`S-LAB` e `R-LAB`), VLANs, Subinterfaces e ACLs. | Validou o alinhamento da topologia simulada com o plano de zonas. |
| **Estudante 1** | Execução dos testes T1-T6, captura de imagens de evidência e revisão final. | Revisou o cumprimento integral dos requisitos e limites de linhas do projeto. |

| Ferramenta | Pergunta ou tarefa solicitada | O que foi aproveitado? | Como a equipe verificou? |
|---|---|---|---|
| Assistente IA | Auxílio na revisão técnica do plano IPv4, formatação Markdown e contagem de palavras da síntese. | Estruturação de respostas dentro dos limites impostos pelo template. | Verificação manual de cada resposta e validação dos testes no Packet Tracer. |

---

## 14. Checklist de entrega

- [x] O Markdown está preenchido de forma sucinta.
- [x] A estimativa do laboratório real inclui duas máquinas dos professores.
- [x] O cálculo de portas inclui uplink e reserva.
- [x] O arquivo `.pkt` abre sem erro.
- [x] Dispositivos possuem nomes legíveis.
- [x] Não há conflito de endereços IP.
- [x] Professor e técnico alcançam as máquinas previstas.
- [x] O Aluno A alcança `IA-A`, mas não `IA-B` nem as máquinas dos professores.
- [x] O usuário comum do campus não inicia acesso ao laboratório.
- [x] Os seis testes estão registrados.
- [x] Há exatamente três evidências visuais.
- [x] A síntese possui entre 80 e 120 palavras.
- [x] Nenhum dado real ou credencial do IFMA foi incluído.

---

## 15. Critérios de avaliação

| Critério | Pontos |
|---|---:|
| requisitos e matriz de permissões | 1,5 |
| dimensionamento, portas e reserva | 1,0 |
| topologia e organização das zonas | 1,5 |
| endereçamento e segmentação | 1,5 |
| regras de acesso e ACLs | 2,0 |
| seis testes e três evidências | 1,5 |
| distinção entre Linux hospedeiro e contêineres | 0,5 |
| clareza, síntese e participação da equipe | 0,5 |
| **Total** | **10,0** |