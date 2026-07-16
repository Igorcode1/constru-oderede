# Atividade Prática - Infraestrutura de Redes

## 📌 Topologia e IPs do Laboratório

* **Servidor**: `192.168.10.100` / Máscara `255.255.255.0`
* **PC3**: `192.168.10.12` / Máscara `255.255.255.0`
* **Switch**: Catalyst 2960 interconectando todos os dispositivos.

## 🛠️ Resolução do Problema

O erro inicial de envio e recebimento de mensagens ocorria porque o simulador do Packet Tracer estava travado no modo **Simulation** (Simulação). 

Ao alternar o simulador para o modo **Realtime** (Tempo Real) e realizar o comando `ping` através do terminal do PC3, a comunicação foi estabelecida com sucesso.

### Resultado do Comando Ping

```bash
Pinging 192.168.10.100 with 32 bytes of data:
Reply from 192.168.10.100: bytes=32 time=3ms TTL=128
Reply from 192.168.10.100: bytes=32 time=1ms TTL=128

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
