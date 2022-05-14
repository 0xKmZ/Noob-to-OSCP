# SNMPWalk Cheatsheet
SNMP protocol provides useful features to monitor and configure network and server systems remotely. Monitoring features are much popular than configuration. snmpwalk is a function provided by SNMP protocol to get metrics of remote system in bulk.

**[+] Get All OIDS**

We will first look the simplest usage of the snmpwalk command. We just provide minimum options to the snmpwalk. We will provide following options as minimum -v 2c version information 2 community -c the public or private secret IPADDRESS

`` snmpwalk -v 1/2c/3 -c public localhost [IP]``

**[+] Write to txt file**

`` snmpwalk -v 1/2c/3 -c public localhost [IP] >> output.txt ``
