## Rotas
```
ip route list
```
## Monitoramento
Acompanha o estado, endereços e rotas dos devices da maquina:
```
sudo ip monitor
```
## Vlan
```
sudo ip link add link enx00e04c680c91 name eth99.20 type vlan id 20
```
```
sudo ip addr add 10.0.60.50/24 dev eth99.20
```
```
sudo ip link set up eth99.20
```
## setando um IPv6
```
ip -6 addr add 2001:db8::55/64 dev eth0
```
## setando MTU
```
sudo ip link set eth0 mtu 1400
```
## Portas em uso
```
netstat -antup
```
```
netstat -atn
```
## Analise de pacotes
```
sudo tcpdump -i eth0 udp port 67 or udp port 68 -n -A -X
```
```
sudo tcpdump -i  udp port 10001 -n -A -X
```
```
sudo tcpdump -i eth0 -w /tmp/test.tcap
```
```
wireshark /tmp/test.tcap
```
## Rotas e IPs
```
nslookup google.com
```
## Scan de SSIDs no WIFI
```
sudo iw dev wlp0s20f3 scan | grep SSID:
```
## DNS
```
nmcli dev show | grep IP6.DNS
```
## Comandos uteis
### Desativando interface
```
sudo ip link set enx00e04c680c91 down
```
### Renomeando interface
```
sudo ip link set enx00e04c680c91 name eth0
```
### Ativando Interface
```
sudo ip link set eth0 up
```
### Adicionando IP a um interface
```
sudo ip addr add 10.10.60.50/24 dev eth0
```

## DHCP
```
sudo vi /etc/dhcp/dhcpd.conf
```
```
sudo service isc-dhcp-server stop
```
```
sudo service isc-dhcp-server start
```
