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

! comment: banner Massage Of The Day
banner motd *UNAUTHORIZED ACCESS IS SUBJECT TO JAIL TIME*!!!
username admin password Simba
ip domain-name simba.co.ke

! comment: Password for console 0
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
```
