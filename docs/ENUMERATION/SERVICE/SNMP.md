# SNMP
#nmap 

``` bash
sudo nmap -sU --open -p 161 192.168.50.1-254 -oG open-snmp.txt
```

#onesixtyone

``` bash
echo public > community
echo private >> community
echo manager >> community
for ip in $(seq 1 254); do echo 192.168.50.$ip; done > ips
onesixtyone -c community -i ips
```

#ENUM_mib 
``` bash
snmpwalk -c public -v1 -t 10 192.168.50.151
-c community string(usually public)
-v snmp version number
-t timeout(seconds)

snmpwalk -c public -v1 192.168.50.151 [MIB sub-tree]
1.3.6.1.4.1.77.1.2.25 local users
1.3.6.1.2.1.25.4.2.1.2 running processes
1.3.6.1.2.1.25.6.3.1.2 installed software
1.3.6.1.2.1.6.13.1.3 listening TCP ports
```