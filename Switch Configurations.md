# Basic Switch Configurations
The following commands were used to configure Hostname, Username, password and domain name on the DMZ-switch.
These commands were copied to help configure the other switches and the VoIP-Router. I just changed the hostname to the respective switch/Router name i.e simba-assess-switch_1, VoIP-Router, simba-core-switch etc.

**Note**: Comments in Cisco CLI are done like this:
**! This is a comment explaining the purpose of the following configuration**

```
enable
configure terminal
hostname DMZ-switch
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
```
### Disabling IP Domain look up and Encrypting Passwords

```
no ip domain-lookup
service password-encryption 
do write

```

## Vlan configuration
The following commands were used to configure Vlans on simba-assess-switch_1, simba-assess-switch_2 and simba-assess-switch_3

```
vlan 50
name LAN
vlan 60
name WLAN
vlan 101
name voIP

! **To see the vlans created**
do show vlan

! **Assigning ports to vlans**
interface range fa0/3-11
switchport mode access
switchport access vlan 50
switchport voice vlan 101
exit

int range fa0/12
switchport mode access
switchport access vlan 60

int range fa0/13-23
switchport mode access
switchport access vlan 50
switchport voice vlan 101
exit

int range fa0/24
switchport mode access
switchport access vlan 60
exit

do write

! **To see the vlans and assigned ports**
show ip interface brief


```
### Core switch Configurations
```
vlan 50
name LAN
vlan 60
name WLAN
vlan 101
name voIP

! **To see the vlans created**
do show vlan

! **Assigning ports to vlans**
! **The Wireless Lan Controller (WLC) should be in the same vlan as the Light Access Points(LAP)**
int Gig1/0/2
switchport mode access
switchport access vlan 60
exit

do write
```
## Configuring EtherChannel, STP Portfast and BPDUguard.
These commands were copied to help configure the other simba-assess-switch_1, simba-assess-switch_2 and simba-assess-switch_3. I just changed the channel-group  & port-channel to 2 and 3 respectively. 

#### Simba-assess-switch_1
```
int range fa0/1-2
channel-group 1 mode active
exit

int port-channel 1
switchport mode trunk
exit

int range fa0/3-24
spanning-tree portfast
spanning-tree bpduguard enable
exit
do write

! **view configurations**
do show start
```

#### Simba-assess-switch_2
```
int range fa0/1-2
channel-group 2 mode active
exit

int port-channel 2
switchport mode trunk
exit

int range fa0/3-24
spanning-tree portfast
spanning-tree bpduguard enable
exit
do write
```

#### Simba-assess-switch_3
```
int range fa0/1-2
channel-group 3 mode active
exit

int port-channel 3
switchport mode trunk
exit

int range fa0/3-24
spanning-tree portfast
spanning-tree bpduguard enable
exit
do write
```
### Simba-Core-switch
Configure EtherChannel, STP Portfast, BPDUguard and Trunk for the Core Switch
```
! **From simba-assess-switch_1**
interface range gig1/0/4-5
channel-group 1 mode active
exit

interface port-channel 1
switchport mode trunk
exit

! **From simba-assess-switch_2**
interface range gig1/0/6-7
channel-group 2 mode active
exit

interface port-channel 2
switchport mode trunk
exit

! **From simba-assess-switch_3**
interface range gig1/0/8-9
channel-group 3 mode active
exit

interface port-channel 3
switchport mode trunk
exit

! **Connects to Cisco-Voice-Gateway Router**
! **This is trunk to allow passage of multiple vlan**
interface range gig1/0/3
switchport mode trunk
exit
```

## Assigning Ip Addresses to Simba-Core-Switch 

```
! **This command was used to assign an Ip address to the interface facing the Firewall
! **The no switchport command switches the port from layer 2 to layer 3
interface gig1/0/1
no switchport
ip address 10.30.30.2 255.255.255.252
exit
do write
```
## Inter-VLAN routing and ip dhcp helper addresses.
The following commands were done on **Simba-Core-Switch**. 
Ip helper address allows the host devices to reach the DHCP Server (10.10.10.3). This would help the host machines to contact DHCP to gain IP addresses.

```
! **Inter-vlan routing SVI(Switched Virtual Interface)**
int vlan 50
no shut
ip address 192.168.10.1 255.255.255.0
ip helper-address 10.10.10.3
exit

int vlan 60
no shut
ip address 10.20.0.1 255.255.0.0
ip helper-address 10.10.10.3
exit

do write
```
## OSPF configuration on the firewall, routers and switch



