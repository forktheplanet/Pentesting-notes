# 139/445 - NetBIOS/SMB

### NetBIOS/Server Message Block

NetBIOS listens on TCP 139 and several UDP ports. SMB \(TCP 445\) and NetBIOS are separate protocols; however, modern implementations of SMB often utilize NetBIOS over TCP for backwards compatibility. SMB has a history of vulnerabilities but we are primarily interested in SMB for enumeration of shares to search for credentials, backups and other information that may help us gain a foothold.

We can search for NetBios/SMB hosts using nmap:

```text
nmap -v -p 139,445 10.11.1.1-254 
sudo nbtscan -r 10.11.1.0/24 
```

#### NSE scripts

```text
nmap -p 139,445 --script=smb* 10.11.1.75
nmap --script=smb-enum* 10.11.1.227
nmap -p 139,445 --script=smb-enum-users 10.11.1.75
nmap -v -p 139,445 -oG smb.txt 10.11.1.1-245 –open
nmap --script smb-vuln-* 10.10.10.40
```

### smbclient

```text
smbclient -L \\$ip\\
smbclient -L \\\\$ip\\
smbclient -L \\\\$ip\\$share
```

### enum4linux

```text
enum4linux 10.11.1.127
enum4linux -a -v 10.11.1.227
```

### showmount

```text
showmount -e $targetip
```

### mount

```text
mount -t cifs -o username=user,password=password //x.x.x.x/share /mnt/share
```

### Download shares

```text
get log.txt --allows you to download single files
smbget -R smb://ipaddress/sharename
```

### smbclient.py

```text
python3 /opt/impacket/examples/smbclient.py username@target-ip
python3 /opt/impacket/examples/smbclient.py 'username'@target-ip
python3 /opt/impacket/examples/smbclient.py ''@target-ip
```

### Eternal Blue

* Metasploit module available, search MS17-010 in MSFconsole
* Manual - [https://github.com/3ndG4me/AutoBlue-MS17-010](https://github.com/3ndG4me/AutoBlue-MS17-010)
* Link includes a python script to check for vulnerability **eternal\_checker.py**

