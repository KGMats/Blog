# Busca inicial pelos containers:

## Resultado NMap

Starting Nmap 7.99 ( https://nmap.org ) at 2026-04-21 16:35 -0300
Nmap scan report for 10.141.22.131
Host is up (0.17s latency).
MAC Address: A4:63:A1:17:7A:4A (Inventus Power Eletronica do Brasil Ltda)
Nmap scan report for 10.141.22.203
Host is up (0.0069s latency).
MAC Address: 3A:2D:66:96:14:A5 (Unknown)
Nmap scan report for 10.141.22.204
Host is up (1.5s latency).
MAC Address: 34:CF:F6:6C:55:11 (Intel Corporate)
Nmap scan report for 10.141.22.227
Host is up (0.078s latency).
MAC Address: A4:63:A1:06:96:9F (Inventus Power Eletronica do Brasil Ltda)
Nmap scan report for 10.141.22.3
Host is up.
Nmap done: 255 IP addresses (5 hosts up) scanned in 16.33 seconds


Vamos investigar cada um dos hosts

Nmap scan report for 10.141.22.131
Host is up (0.011s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE
80/tcp   open  http
2121/tcp open  ccproxy-ftp
2222/tcp open  EtherNetIP-1
4445/tcp open  upnotifyp
7070/tcp open  realserver
8080/tcp open  http-proxy
MAC Address: A4:63:A1:17:7A:4A (Inventus Power Eletronica do Brasil Ltda)

Nmap done: 1 IP address (1 host up) scanned in 7.76 seconds



