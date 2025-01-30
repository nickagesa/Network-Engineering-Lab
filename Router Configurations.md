# Basic Switch Configurations
The following commands were used to configure Hostname, Username, password and domain name on the VoIP-Router.

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
```
