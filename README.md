# Atividade de Redes - Teste de Conectividade

## Topologia da Rede
* **Servidor**: IP `192.168.10.100` / Máscara `255.255.255.0`
* **PCs**: IPs de `192.168.10.10` a `192.168.10.12`
* **Interconexão**: Conectados através de um Switch Catalyst 2960.

## Resolução do Problema
O erro inicial de envio de mensagens ocorria porque o simulador estava no modo **Simulation** (com o tempo pausado). 
Ao alternar para o modo **Realtime** e testar a comunicação via Prompt de Comando, os pacotes foram transmitidos com sucesso.

### Resultado do Teste de Ping (PC3 para Servidor):
```bash
Pinging 192.168.10.100 with 32 bytes of data:
Reply from 192.168.10.100: bytes=32 time=3ms TTL=128
Reply from 192.168.10.100: bytes=32 time=1ms TTL=128

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)