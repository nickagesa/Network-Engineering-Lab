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

## OSPF configuration on the firewall, routers and switch
We advertised 3 networks Inside Zone, DMZ and Outside Zone. 
There is no need to use wild cards in firewall, since it only uses subnet mask.
```
ip routing
router ospf 35
router-id 1.1.3.3
network 10.30.30.0 255.255.255.252 area 0
network 10.10.10.0 255.255.255.240 area 0
network 197.200.100.0 255.255.255.252 area 0

exit
write memory
```

## Firewall inspection policy configuration and NAT
By default fire wall denies any traffic to go through it unless allowed.
I first configured NAT to allow for internet connection.

```
! **Enable NAT (You create object networks)**
! **LAN Network to access internet**

object network INSIDE-OUTSIDE
subnet 192.168.10.0 255.255.255.0
nat (INSIDE,OUTSIDE) dynamic interface
exit

! **WLAN (Wireless Controller LAN)**

object network INSIDE-OUTSIDE2
subnet 10.20.0.0 255.255.0.0
nat (INSIDE,OUTSIDE) dynamic interface
exit

! **DMZ Network**

object network INSIDE-OUTSIDE3
subnet 10.10.10.0 255.255.255.240
nat (DMZ,OUTSIDE) dynamic interface
exit

! **create a default routing to the ISP**
! **This is for incase the firewall doesn't know where to route a request It would send it to the ISP**
! ** The 0.0.0.0... is to say any Ip Address with any subnetmask**

route OUTSIDE 0.0.0.0 0.0.0.0 197.200.100.1

! *create Inspection policy to enable computers to get DHCP service**
! **we will permit internal clients to send icmp to any machine in dmz also allow udp port 68 & 67 for dhcp, port 53 for DNS, 443, 8443 HTTPS and 80 http etc**


! **Icmp**
access-list INSIDE-DMZ extended permit icmp any any

! **Dhcp**
access-list INSIDE-DMZ extended permit udp any any eq 67
access-list INSIDE-DMZ extended permit udp any any eq 68

! **Dns**
access-list INSIDE-DMZ extended permit udp any any eq 53
access-list INSIDE-DMZ extended permit tcp any any eq 53

! **Http & Https**
access-list INSIDE-DMZ extended permit tcp any any eq 80
access-list INSIDE-DMZ extended permit tcp any any eq 8080
access-list INSIDE-DMZ extended permit tcp any any eq 443
access-list INSIDE-DMZ extended permit tcp any any eq 8443

! **FTP**
access-list INSIDE-DMZ extended permit tcp any any eq 20
access-list INSIDE-DMZ extended permit tcp any any eq 21
access-list INSIDE-DMZ extended permit udp any any eq 21
access-list INSIDE-DMZ extended permit tcp any any eq 989
access-list INSIDE-DMZ extended permit udp any any eq 989
access-list INSIDE-DMZ extended permit tcp any any eq 990
access-list INSIDE-DMZ extended permit udp any any eq 990

! **ssh**
access-list INSIDE-DMZ extended permit tcp any any eq 22
access-list INSIDE-DMZ extended permit udp any any eq 22

! **smtp**
access-list INSIDE-DMZ extended permit tcp any any eq 25
access-list INSIDE-DMZ extended permit tcp any any eq 587

! **POP3**
access-list INSIDE-DMZ extended permit tcp any any eq 110
access-list INSIDE-DMZ extended permit tcp any any eq 995
access-list INSIDE-DMZ extended permit udp any any eq 995

! **IMAP4**
access-list INSIDE-DMZ extended permit tcp any any eq 143
access-list INSIDE-DMZ extended permit udp any any eq 143
access-list INSIDE-DMZ extended permit udp any any eq 993



! **applying these rules to the DMZ interfaces**

access-group INSIDE-DMZ in interface DMZ
write memory


! **allowing connection to Azure**


access-list INSIDE-OUTSIDE permit icmp any any

access-list INSIDE-OUTSIDE permit tcp any any eq 80
access-list INSIDE-OUTSIDE permit tcp any any eq 8080
access-list INSIDE-OUTSIDE permit tcp any any eq 443
access-list INSIDE-OUTSIDE permit tcp any any eq 8443

access-group INSIDE-OUTSIDE in interface OUTSIDE

write memory
```
## Firewall inspection policy configuration and NAT


