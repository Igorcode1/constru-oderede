# Apresentação do Projeto: Rede Corporativa no Cisco Packet Tracer (Simplificado)

---

## 1. O que é este projeto? (Objetivo)

Este projeto simula a criação de uma rede de computadores para uma empresa que possui uma **Matriz** (escritório principal), uma **Filial** (segundo escritório) e precisa se conectar à **Internet**.

O objetivo principal é fazer com que todos os computadores trabalhem de forma organizada, rápida, segura e consigam se comunicar sem falhas.

---

## 2. Como a rede foi organizada?

Imagine a rede dividida em três grandes partes:

1.  **A Matriz:** Onde ficam a maioria dos funcionários (divididos em setores).
2.  **A Filial:** Um escritório menor distante que precisa acessar os dados da Matriz.
3.  **A Internet:** O mundo externo (como acessar o site do Google ou um sistema na nuvem).

---

## 3. Os 5 Passos Práticos para Fazer Funcionar

Para que essa rede funcione perfeitamente, configuramos 5 tecnologias fundamentais. Aqui está a explicação simples de cada uma delas para você apresentar:

### 🖥️ Passo 1: Organização por Setores (VLANs)
*   **O que é:** Em vez de deixar todos os computadores misturados, dividimos a rede da Matriz em "setores virtuais". Criamos um setor para o **Administrativo** e outro para o **Financeiro**.
*   **Por que fazer isso?** Segurança e organização. O setor Financeiro não precisa ficar recebendo arquivos ou bisbilhotando o tráfego do setor Administrativo.

### 🔌 Passo 2: Distribuição Automática de Internet (DHCP)
*   **O que é:** Configuramos o roteador para entregar o "endereço de rede" (IP) para cada computador de forma totalmente automática.
*   **Por que fazer isso?** Para não ter que ir de computador em computador digitando números manualmente. É só ligar o computador na tomada de rede e ele já sai navegando.

### 🗺️ Passo 3: Conexão entre os Setores (Roteamento Inter-VLAN)
*   **O que é:** Embora os setores (VLANs) estejam separados para segurança, às vezes eles precisam conversar (por exemplo, enviar um documento do Administrativo para o Financeiro).
*   **Como funciona:** Usamos o roteador como um "guarda de trânsito" (chamado tecnicamente de *Router-on-a-Stick*). Ele é o único que tem permissão para autorizar e levar dados de um grupo para o outro.

### 🌐 Passo 4: Ligação com a Filial (OSPF)
*   **O que é:** Configuramos um protocolo inteligente de conversa entre o roteador da Matriz e o da Filial (chamado **OSPF**).
*   **Como funciona:** Esses dois roteadores conversam entre si e aprendem sozinhos o melhor caminho para enviar as informações do escritório principal para a filial, de forma rápida e automática.

### 🛡️ Passo 5: Acesso Seguro à Internet (NAT)
*   **O que é:** Os computadores da empresa usam "endereços internos/privados" que não podem navegar direto na internet pública. O **NAT** funciona como um tradutor ou um "único número de telefone externo" da empresa.
*   **Como funciona:** Quando alguém de dentro quer acessar um site na internet, o roteador esconde o IP real do computador e usa um IP público para buscar a informação de forma segura.

---

## 4. Como provamos que tudo funciona? (Os Testes)

Se alguém perguntar como você sabe que deu certo, você pode explicar estes 3 testes simples:

1.  **Pegando o IP:** Ligamos o computador e ele recebeu as configurações sozinho (o DHCP funcionou).
2.  **Conversando entre computadores (Ping):** Fizemos o teste de mandar um sinal ("ping") do computador do Administrativo para o do Financeiro, e a resposta foi instantânea (a comunicação interna funcionou).
3.  **Acessando a Internet:** Simulamos a abertura de uma página web a partir de um computador interno, provando que o tradutor de internet (NAT) está funcionando perfeitamente.

---

## 5. Resumo para a sua Apresentação (Conclusão)

> *"Senhores, este projeto no Packet Tracer representa uma rede moderna e real. Nós conseguimos separar os departamentos para garantir **segurança**, automatizamos a entrega de internet para trazer **praticidade**, conectamos a filial para manter o **negócio integrado** e tudo isso funcionando com acesso **seguro à internet**. É uma estrutura profissional, barata de manter e pronta para crescer."*

---
*Dica para a apresentação: Foque em explicar o "Por que" de cada tecnologia e use as analogias (guarda de trânsito, telefone central, gavetas organizadas).*