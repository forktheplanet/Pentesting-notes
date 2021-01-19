# Windows privilege escalation

## Manual enumeration

### User

```text
whoami
net user username
```

### Other Users

```text
net user
```

### Privileges

```text
whoami /priv
```

### Hostname

```text
hostname
```

### OS and architecture

```text
systeminfo
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

### Processes and services

```text
tasklist /SVC
```

### Network

```text
ipconfig /all (interfaces)
route print (routing table)
netstat -ano (active connections)
arp -a
```

### Firewall/AV status

```text
sc query windefend
sc query type=service
netsh
netsh advfirewall show rule name -all
netsh advfirewall dump
netsh firewall show state
netsh advfirewallshow currentprofile
```

### Applications/patch levels/drivers/kernel modules

```text
wmic product get name
wmic product get version
wmic product get vendor
wmic product get name, version, vendor
wmic qfe
wmic qfe get Caption, Description, HotFixID, InstalledOn
(PS) driverquery.exe /v /fo csv |ConvertFrom -CSV | Select-Object 'Display Name', 'Start Mode', Path
(PS) Get-WmiObject Win32_PnPSignedDriver | Select-Object DeviceName, DeviceVersion, Manufacturer | Where-Object {$_.DeviceName -like "*VMWare*"} 
```

### Readable/writeable directories

```text
accesschk.exe -uws "Everyone" "C:\Program Files"   (SysInternalsSuite)
(PS) Get-ChildItem "C:\Program Files" -Recurse | Get-ACL | ?{$_.AccessToString-match "Everyone\sAllow\s\sModify"}
```

### Mounted/unmounted disks

```text
mountvol
wmic logicaldisk
list drives
```

### Passwords

```text
findstr /si password *.txt
findstr /si password *.xml
findstr /si password *.ini
dir /s *pass* == *cred* == *vnc* == *.config*
findstr /spin “password” *.*
```

### Scheduled tasks

```text
schtasks /query /fo LIST /v
```

### Binaries that auto elevate

```text
reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer
reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer
```

## Automated tools

```text
winPEAS.exe
PowerUp.ps1
windows-exploit-suggester.py
Metasploit - post/multi/recon/local_exploit_suggester
```

### windows-exploit-suggester.py

* Run `systeminfo` and save the output into a text document 
* Update the database - `./windows-exploit-suggester.py --update` 
* .`/windows-exploit-suggester.py --database DBNameHere --systeminfo filepath.txt`

### Metasploit exploit suggester

* Background session `background`
* Select exploit to use
* Set Session
* Set LHOST and LPORT
* Run

