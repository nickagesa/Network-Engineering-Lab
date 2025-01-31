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
We Only advertise networks connected to the router.

### Zuku Router
```
ip routing
router ospf 35
router-id 1.1.4.4
network 197.200.100.0 0.0.0.3 area 0
network 20.20.20.0 0.0.0.3 area 0
exit
do write
```

### Azure Router
```
ip routing
router ospf 35
router-id 1.1.5.5
network 20.20.20.0 0.0.0.3 area 0
network 30.30.30.1 0.255.255.255 area 0
exit
do write
```

## Telephony service configuration (cisco - voice Gateway Router)
```
interface fa0/0
no shut
exit

interface fa0/0.101
encapsulation dot1q 101
ip address 172.16.10.1 255.255.255.0
exit

service dhcp
ip dhcp pool VOIP
network 172.16.10.0 255.255.255.0
option 150 ip 172.16.10.1
exit

do write

telephony-service
max-ephones 10
max-dn 10

ip source-address 172.16.10.1 port 2000
auto assign 1 to 10

! **Allocating IP Phones Dial Numbers**
ephone-dn 1
number 1001
exit

ephone-dn 2
number 1002
exit

ephone-dn 3
number 1003
exit

ephone-dn 4
number 1004
exit

ephone-dn 5
number 1005
exit

ephone-dn 6
number 1006
exit

ephone-dn 7
number 1007
exit

ephone-dn 8
number 1008
exit

ephone-dn 9
number 1009
exit

ephone-dn 10
number 1010
```
