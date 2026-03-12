# iptables Cheat Sheet

iptables is a Linux command line utility for configuring host-based firewall settings.  

## Filter Chains
  
| Chain | Description |
|--------|------------|
|INPUT|  Inbound datagrams |
|FORWARD| Datagrams being routed through the host (i.e. from one network to another) |
|OUTPUT| Outbound datagrams |

## Targets
  
| Target | Description |
|--------|-------------|
| ACCEPT | Datagrams are accepted when received |
| DROP | Datagrams are dropped when received (i.e. do nothing) |
| REJECT | Datagrams are refused when received |
  
## Protocols  

|Protocol| Description |
|---------|-------------|
|tcp     | Transmission Control Protocol         |
|udp     | User Datagram Protocol          |
|icmp | Internet Control Message Protocol            |
  
## Commands  
  
|   Command  | Description  |
|------------|----------------|
|`iptables -nL` |List INPUT/ FORWARD/ OUTPUT rules (with numeric output)|
|`iptables -nL -t nat` | List PREROUTING/  POSTROUTING NAT rules |
|`iptables -F `|Flush (delete) all rules|
|`iptables -P [INPUT/FORWARD/OUTPUT] [ACCEPT/DROP]` |Set the default policy (e.g. DROP) of a chain (e.g. INPUT)|
|`iptables -A <chain> -p <protocol> -s <source IP> --dport <destination port> -j <target>` | Appends a rule to the chain regulating traffic of a specific protocol from a source IP to a destination port |
|`iptables -A <chain> -d <destination IP> --sport <source port> -j <target>` | Appends a rule the chain regulating traffic to a destination IP address from a specific source port |
|`sudo iptables -D <chain> <entry_num>` | Delete a rule from a chain |

## Examples  
  
| Description | Command |
|-------------|---------|
| Enable inbound logging | `sudo iptables -A INPUT -j LOG` |
| Check all logs | `cat /var/log/messages` |
| Check most recent logs | `tail /var/log/messages` |
| Prefix logs for inbound ICMP (pings) | `sudo iptables -A INPUT -p icmp -j LOG --log-prefix "Ping detected"`
| Log inbound HTTP traffic | `sudo iptables -A INPUT -p tcp --dport 80 -j LOG` |
| Forward incoming traffic on port 22 to port 2222 | `sudo iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 2222` |
| Forward incoming traffic on port 23 to port 2223 | `sudo iptables -t nat -A PREROUTING -p tcp --dport 23 -j REDIRECT --to-port 2223` |
| Save iptables entries | `sudo iptables-save > /etc/sysconfig/iptables` |


