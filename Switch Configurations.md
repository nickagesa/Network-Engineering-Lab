# Basic Switch Configurations
The following commands were used to configure Hostname, Username, password and domain name on the DMZ, .

```
enable
configure terminal
hostname DMZ switch
enable password Simba
banner motd *UNAUTHORIZED ACCESS IS SUBJECT TO JAIL TIME*!!!
username admin password Simba
ip domain-name simba.co.ke
line console 0
password Simba
login
exit
no ip domain-lookup
service password-encryption
do write


vlan 50
name LAN
vlan 60
name WLAN
vlan 101
name voIP

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
