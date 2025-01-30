# Basic Router Configurations
The following commands were used to configure Hostname, Username, password and domain name on the VoIP-Router.

### voIP Router
```
enable
configure terminal
hostname voIP_Router
enable password Simba

! **Banner Massage Of The Day**
banner motd *UNAUTHORIZED ACCESS IS SUBJECT TO JAIL TIME*!!!
username admin password Simba
ip domain-name simba.co.ke

! **Password for console 0**
line console 0
password Simba
login
exit

no ip domain-lookup
service password-encryption
do write

```
### Zuku Router
```
enable
configure terminal
interface GigabitEthernet0/0
no shut
ip address 197.200.100.1 255.255.255.252
exit

interface GigabitEthernet0/1
no shut
ip address 20.20.20.1 255.255.255.252
exit

do write
```

### Azure Cloud
```
enable
configure terminal
interface GigabitEthernet0/0
no shut
ip address 20.20.20.2 255.255.255.252
exit

interface GigabitEthernet0/1
no shut
ip address 30.30.30.1 255.0.0.0
exit

do write
```
## OSPF configuration on the firewall, routers and switch

```
ip routing
router ospf 35
router-id 1.1.4.4
network 197.200.100.0 0.0.0.3 area 0
network 20.20.20.0 0.0.0.3 area 0
exit
do write

ip routing
router ospf 35
router-id 1.1.5.5
network 20.20.20.0 0.0.0.3 area 0
network 30.30.30.1 0.255.255.255 area 0
exit
do write
```

