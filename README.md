# IPv6 survival kit
Quick start with IPv6 -> Under construction

### DNS IPV6 ###
Google   
```conf
2001:4860:4860::8888
2001:4860:4860::8844
```

Cloudflare    
```conf
2606:4700:4700::1111
2606:4700:4700::1001
```

Quad9    
```conf
2606:fe::fe
2606:fe::10
```

### In your browser ###   
Example to access on your synology with only IPv6 and port.   
```conf
https://[XXXX::XXX:bce0::2805:4e1d]:5001
```

### Command on Linux ###
Ping to google from IPv6
```bash
ping -6 ipv6.google.com
```

To check your route :   
```bash
ip -6 r
```

To check your ip address :   
```bash
ip -6 a
```

### iptables v6 ###
ip6tables with the same arguments as iptables   
Quick conf 

```bash
IP6T=/sbin/ip6tables
# Clears all current rules. -F all. -X users
$IP6T -t filter -F
$IP6T -t filter -X
$IP6T -t mangle -F
$IP6T -t mangle -X
# default strategy (-P): block all incoming forward and allow outgoing
$IP6T -t filter -P INPUT DROP
$IP6T -t filter -P FORWARD DROP
$IP6T -t filter -P OUTPUT ACCEPT
# Loopback
$IP6T -t filter -A INPUT -i lo -j ACCEPT
$IP6T -t filter -A OUTPUT -o lo -j ACCEPT
# Allow an open connection to receive incoming traffic
$IP6T -t filter -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
# Allow PING
$IP6T -I INPUT 2 -p icmpv6 -j ACCEPT
# DNS:53
$IP6T -t filter -A INPUT -p tcp --dport 53 -j ACCEPT
$IP6T -t filter -A INPUT -p udp --dport 53 -j ACCEPT
```

Apply   
```bash
ip6tables-apply
```
Save   
```bash
ip6tables-save > /etc/iptables/rules.v6
```
At boot   
```bash
nano /etc/network/if-up.d/ip6tables
```
Add this script   
```bash
#!/bin/sh
/sbin/ip6tables-restore < /etc/iptables/rules.v6
```
Make it executable   
```bash
chmod +x /etc/network/if-up.d/ip6tables
```

To check after reboot   
```bash
ip6tables -nvL
```


Fail2ban V6 ?
