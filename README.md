# IPv6 survival kit
Quick start with IPv6 -> Under construction

### DNS Google V6 ###
```conf
2001:4860:4860::8888
2001:4860:4860::8844
```

### On your FREEBOX, precision ###    
Local link IPV6 address is -> your gateway   
You have 8 subnets with /64

### In your browser ###   
Example to access on your synology with only IPv6 and port.   
```conf
https://[XXXX::XXX:bce0::2805:4e1d]:5001
```

### Command in Linux ###
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
# DNS:53
$IP6T -t filter -A INPUT -p tcp --dport 53 -j ACCEPT
$IP6T -t filter -A INPUT -p udp --dport 53 -j ACCEPT
```
