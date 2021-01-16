# 25 - SMTP

We can attempt to enumerate SMTP by attempting to connect, then using basic commands to gather information.

### Connecting

```text
nc -nv $targetip 25
telnet $targetip 25
```

### Enumeration

```text
VRFY user- asks the server to verify an email address
EXPN - asks the server for the membership of a mailing list
```

