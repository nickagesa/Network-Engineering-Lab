# Basic Switch Configurations
The following commands were used to configure Hostname, Username, password and domain name on the DMZ-switch.
These commands were copied to help configure the other switches and the VoIP-Router. I just changed the hostname to the respective switch/Router name i.e simba-assess-switch_1, VoIP-Router, simba-core-switch etc.

**Note**: Comments in Cisco CLI are done like this **! This is a comment explaining the purpose of the following configuration**

```
enable
configure terminal
hostname DMZ-switch
enable password Simba

! command: banner Massage Of The Day
banner motd *UNAUTHORIZED ACCESS IS SUBJECT TO JAIL TIME*!!!
username admin password Simba
ip domain-name simba.co.ke

! command: password for console 0
line console 0
password Simba
login
exit
```
## Disabling IP Domain look up and Encrypting Passwords

```
no ip domain-lookup
service password-encryption 
do write

```
