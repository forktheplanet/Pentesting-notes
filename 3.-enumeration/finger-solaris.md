# Finger \(Solaris\)

List users

```text
finger @$TargetIP
```

Query for existence of specific users

```text
finger root@$TargetIP
```

Brute force enumerate users

Download pentestmonkey's enumeration script:

{% embed url="https://github.com/pentestmonkey/finger-user-enum" %}

```text
perl finger_user_enum.pl -U /usr/share/wordlists/Users.txt -t $TargetIP
```

