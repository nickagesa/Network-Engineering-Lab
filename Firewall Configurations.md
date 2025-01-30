# Basic Configurations
The following commands were used to configure Hostname, Username, password and domain name.

```
enable
configure terminal
hostname Perimeter-FireWall
enable password Simba
username admin password Simba
domain-name simba.co.ke

write memory
```
## Defining Firewall Zones
These commands were used to assign names, security level and ip addresses to different zones
```
interface gig1/1
no shut
nameif INSIDE
security-level 100
ip address 10.30.30.1 255.255.255.252
exit

interface gig1/2
no shut
nameif DMZ
security-level 70
ip address 10.10.10.1 255.255.255.240
exit

interface gig1/3
no shut
nameif OUTSIDE
security-level 0
ip address 197.200.100.2 255.255.255.252
exit

write memory

```
