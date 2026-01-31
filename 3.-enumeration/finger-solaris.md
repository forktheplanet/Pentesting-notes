# Finger (Solaris)

List users

```
finger @$TargetIP
```

Query for existence of specific users

```
finger root@$TargetIP
```

Brute force enumerate users

Download pentestmonkey's enumeration script:

{% embed url="https://github.com/pentestmonkey/finger-user-enum" %}

```
perl finger_user_enum.pl -U /usr/share/wordlists/Users.txt -t $TargetIP
```
