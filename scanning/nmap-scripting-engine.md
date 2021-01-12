# Nmap Scripting Engine

Scripts stored in: /usr/share/nmap/scripts

```text
locate *.nse | grep smb
```

Banner grabbing: 

```text
nmap --script banner 10.10.10.5
```

Vulnerability scanning: 

```text
nmap -sV --script vulners [--script-args mincvss=<arg_val>] <target>
nmap --script vuln 10.10.10.5
nmap -p 139,445 --script=$scriptname $targetip
```

With wildcards:

```text
nmap -p 139,445 --script=smb-vuln* $targetip
nmap -v -p 21 --script=ftp-anon.nse 10.11.1.1-254
nmap -v -p 139, 445 --script=smb-security-mode 10.11.1.236
```

