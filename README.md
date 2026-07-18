# 🌐 Repositório de Redes de Computadores — info-200

<p align="center">
  <img src="https://img.shields.io/badge/IFMA-Campus%20Itapecuru--Mirim-green?style=for-the-badge" alt="IFMA">
  <img src="https://img.shields.io/badge/Curso-T%C3%A9cnico%20em%20Inform%C3%A1tica-blue?style=for-the-badge" alt="Informática">
  <img src="https://img.shields.io/badge/Turma-info--200-orange?style=for-the-badge" alt="info-200">
</p>

---

## 👋 Bem-vindo ao Nosso Hub de Conectividade!

Seja muito bem-vindo ao nosso quartel-general de estudos, relatórios e simulações práticas da matéria de **Redes de Computadores** do Instituto Federal do Maranhão (IFMA). 

Aqui, nós deciframos os mistérios de como os dados viajam pelo mundo em milissegundos, transformando cabos, ondas de rádio e placas de silício em mágica funcional.

---

## 🎨 Mapa da Nossa Rede Mental (Topologia Conceptual)

Para ilustrar como enxergamos a matéria, preparamos este desenho de arquitetura de rede que representa a jornada do nosso aprendizado:

```text
               ╔═════════════════════════════════════════════════╗
               ║               ☁️ A GRANDE INTERNET ☁️             ║
               ║          (Onde tudo acontece e se conecta)      ║
               ╚═════════════════════════════════════════════════╝
                                        │
                                        ▼ [Camada 3: Rede]
                               ┌─────────────────┐
                               │  📌 ROTEADOR    │ ◄─── (Lê IPs, escolhe caminhos
                               └────────┬────────┘       e interconecta mundos!)
                                        │
                                        ▼ [Camada 2: Enlace]
                               ┌─────────────────┐
                               │  🎛️ SWITCH     │ ◄─── (O mestre da LAN! Lê MACs,
                               └──────┬─┬─┬──────┘       evita colisões e organiza tudo)
                                      │ │ │
                 ┌────────────────────┘ │ └────────────────────┐
                 ▼                      ▼                      ▼
            ┌─────────┐            ┌─────────┐            ┌─────────┐
            │ 💻 PC 1 │            │ 💻 PC 2 │            │ 💻 PC 3 │
            ├─────────┤            ├─────────┤            ├─────────┤
            │  IGOR   │            │  CAUÃ   │            │ RENATO  │
            └─────────┘            └─────────┘            └─────────┘
         [192.168.10.10]        [192.168.10.20]        [192.168.10.30]
         
         └──────────────────────────────┬──────────────────────────────┘
                                        ▼
                         ⚡ [Camada 1: Física (Bits)]
               (Cabos trançados, conectores RJ-45 e pura energia!)