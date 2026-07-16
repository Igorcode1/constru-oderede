# Trilha guiada — Entrega D0: projeto inicial da rede

## Identificação

| Campo | Resposta da equipe |
|---|---|
| Nome da equipe | **Equipe Calango** |
| Integrantes | **Igor, Renato e Cauã** |
| Turma | **INFO-200** |
| Nome do projeto | Conectividade do Centro de Memórias Quilombolas |
| Data | **16/07/2026** |

---

## 4. Cenário acadêmico de referência

### Cenário adotado pela equipe

> **Resposta da equipe:** Utilizaremos o cenário de referência: Centro de Tecnologia e Memórias Comunitárias, com a necessidade de interligar a administração, o laboratório (com suporte a 20 computadores), acesso sem fio para professores e visitantes, e o servidor local.

---

# Parte A — Compreensão do problema

## 5. Escreva o problema

### Problema formulado pela equipe

> No contexto do **Centro de Tecnologia e Memórias Comunitárias**, os **estudantes, professores, administradores e visitantes** precisam **acessar o servidor local do Mapa de Memórias e a Internet**, mas **atualmente não existe uma rede local estruturada e o limite de portas físicas de um único switch padrão de mercado impossibilita a expansão e conexão segura de todos os dispositivos cabeados e sem fio**[cite: 1, 2, 3], o que prejudica **as aulas práticas, as pesquisas científicas e a gestão diária do centro**.

---

## 6. Identifique os usuários

| Grupo de usuários | Quantidade estimada | O que precisa fazer na rede | Prioridade |
|---|---:|---|---|
| **Administração** | 1 a 2 | Gerenciar o centro e imprimir documentos institucionais[cite: 3] | alta[cite: 3] |
| **Estudantes** | 20 | Pesquisar no laboratório e acessar o Mapa de Memórias[cite: 3] | alta[cite: 3] |
| **Professores** | 5 a 10 | Acessar rede via notebooks para conduzir aulas[cite: 3] | alta[cite: 3] |
| **Visitantes** | Variável | Navegar na internet por dispositivos móveis[cite: 3] | baixa[cite: 3] |

### Quem administrará ou manterá a rede?

> **Resposta da equipe:** O técnico de laboratório local ou a equipe de suporte central de tecnologia da informação[cite: 3].

---

## 7. Identifique os setores ou ambientes

| Setor ou ambiente | Usuários atendidos | Dispositivos previstos | Necessidades principais |
|---|---|---:|---|
| **Laboratório** | Estudantes | 20 PCs[cite: 3] | Acesso cabeado rápido e estável ao servidor local[cite: 3]. |
| **Administração** | Equipe Administrativa | 1 PC, 1 Impressora[cite: 3] | Acesso restrito a arquivos de gestão e impressão[cite: 3]. |
| **Área Comum** | Professores e Visitantes | Laptops e Celulares[cite: 3] | Cobertura de sinal sem fio e navegação segura[cite: 3]. |
| **Sala Técnica** | Administrador de TI | 1 Servidor, Roteador, Switches | Hospedagem segura dos dados e distribuição da rede. |

### Há ambientes, distâncias ou obstáculos que ainda precisam ser conhecidos?

> **Resposta da equipe:** Precisamos validar a planta arquitetônica física para estimar possíveis perdas de atenuação de sinal de radiofrequência das paredes e verificar se o limite de 100 metros para cabos UTP categoria 5e/6 será respeitado.

---

## 8. Liste necessidades e serviços

| Usuário ou setor | Necessidade | Serviço relacionado | Importância | Como saberemos que funciona? |
|---|---|---|---|---|
| **Estudantes/Lab** | Acessar o Mapa de Memórias | Serviço HTTP (Servidor local) | alta[cite: 3] | O site será renderizado no navegador de qualquer PC. |
| **Visitantes** | Conectar celulares à Internet | Acesso Wi-Fi e roteamento[cite: 3] | baixa[cite: 3] | Celulares receberão endereço lógico e carregarão sites externos[cite: 3]. |
| **Administração** | Imprimir formulários | Serviço de impressão em rede[cite: 3] | média[cite: 3] | O teste de ping retornará sucesso e folhas serão impressas[cite: 3]. |

---

# Parte B — Da necessidade à proposta

## 9. Selecione recursos e justifique

### Recursos propostos

| Recurso | Quantidade inicial | Necessidade atendida | Justificativa | Dúvida ou premissa |
|---|---:|---|---|---|
| **Roteador de Borda** | 1 | Acesso à Internet[cite: 3] | Equipamento necessário para interligar redes distintas (LAN/WAN). | Premissa: Utilizaremos interface Gigabit. |
| **Switch 24 portas** | 2 | Interligar dispositivos cabeados[cite: 3] | Dois switches 2960 em cascata garantem capacidade de expansão física. | Modelo Cisco Catalyst 2960. |
| **Access Point** | 1 | Conectividade sem fio[cite: 3] | Prover cobertura sem fio local para dispositivos móveis. | Cobrirá a área com barreira de alvenaria? |
| **Servidor** | 1 | Mapa de Memórias[cite: 3] | Hospedar localmente a página web e os dados de memória. | Será usada redundância de discos? |
| **PCs de Mesa** | 21 | Uso geral[cite: 3] | 20 computadores para o laboratório e 1 para a administração[cite: 3]. | Nenhuma no momento. |

### Conferência de capacidade

1. Quantas conexões cabeadas são necessárias inicialmente?
> **Resposta:** São necessárias 25 conexões de acesso direto (20 PCs do laboratório + 1 PC de administração + 1 Impressora de rede + 1 Servidor + 1 Access Point + 1 link com o Roteador de Borda)[cite: 3].

2. Quantas portas deverão ficar livres para expansão?
> **Resposta:** Utilizando dois switches de 24 portas (totalizando 48 conexões de rede), restam 21 interfaces físicas livres para fins de expansão administrativa e novos terminais de pesquisa.

3. A quantidade de portas dos switches propostos é suficiente? Demonstre a conta.
> **Resposta e cálculo:** Sim. 
$$2 \times 24 \text{ (portas físicas)} = 48 \text{ portas disponíveis}$$
[cite: 1]
$$48 \text{ (total)} - 25 \text{ (dispositivos ativos)} - 2 \text{ (portas usadas no link de cascata)} = 21 \text{ portas livres}$$


4. Quais usuários necessitam de Wi-Fi?
> **Resposta:** Professores (notebooks) e Visitantes (dispositivos móveis inteligentes)[cite: 3].

5. A quantidade de access points é conhecida ou ainda depende de levantamento de área, obstáculos e quantidade de usuários?
> **Resposta:** Dependerá diretamente de uma análise de propagação eletromagnética em campo (survey), mas iniciaremos o piloto do projeto com apenas uma unidade central para simulação de canal[cite: 3].

---

## 10. Registre premissas e perguntas em aberto

| Tipo | Premissa ou pergunta | Por que importa? | Como será confirmada? |
|---|---|---|---|
| premissa | O modelo do switch será Cisco 2960. | Garante compatibilidade de comandos de rede no laboratório[cite: 1]. | Consulta ao catálogo de equipamentos[cite: 1]. |
| pergunta | Como isolaremos o tráfego dos visitantes? | Garante que visitantes não acessem dados sigilosos administrativos[cite: 3]. | Implementação de segmentação lógica (VLANs) futuramente[cite: 3]. |

---

# Parte C — Topologia inicial

## 11. Desenhe a topologia

```mermaid
flowchart TD
    ISP["Internet / Provedor"] --- BORDA["Roteador de Borda"]
    BORDA --- SW1["Switch Central 1 (Cisco 2960)"]
    SW1 --- SW2["Switch Central 2 (Cisco 2960)"]
    
    SW1 --- ADM["Administração (1 PC + 1 Impressora)"]
    SW1 --- SRV["Servidor (Mapa de Memórias)"]
    SW1 --- AP["Access Point"]
    
    SW2 --- LAB["Laboratório (20 PCs)"]
    
    AP -. "Wi-Fi" .- PROF["Notebooks (Professores)"]
    AP -. "Wi-Fi" .- VIS["Dispositivos Móveis (Visitantes)"]