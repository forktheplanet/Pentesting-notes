# 161 (UDP) - SNMP

### Simple Network Management Protocol

SNMP is commonly misunderstood resulting in misconfigurations.&#x20;

```
nmap -sU --open -p 161 10.11.1.1-254 
onesixtyone 10.11.1.1/24
```

### snmp-check

```
snmp-check $targetip
```

### snmpwalk

#### V1 enumeration (entire MIB tree)

```
snmpwalk -c public -v1 -t 10 $ipaddress
snmpwalk -c private -v1 -t 10 $ipaddress
snmpwalk -c manager -v1 -t 10 $ipaddress
```

#### Enumeration

```
snmpwalk -c public -v1 $ipaddress 1.3.6.1.4.1.77.1.2.25 (users)
snmpwalk -c public -v1 $ipaddress 1.3.6.1.2.1.25.1.6.0 (processes)
snmpwalk -c public -v1 $ipaddress 1.3.6.1.2.1.25.4.2.1.2 (running programs)
snmpwalk -c public -v1 $ipaddress 1.3.6.1.2.1.25.2.3.1.4 (storage units)
snmpwalk -c public -v1 $ipaddress 1.3.6.1.2.1.6.13.1.3 (tcp local ports)
snmpwalk -c public -v1 $ipaddress 1.3.6.1.2.1.25.6.3.1.2 (software)
```

### onesixtyone

```
onesixtyone -c community -i $targetip
```
