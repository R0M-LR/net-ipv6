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
