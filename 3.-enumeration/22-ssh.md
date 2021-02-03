# 22 - SSH

SSH is not typically vulnerable but it often a candidate for password reuse attacks.  When enumerating you should check for:

* Version info \(banner grab\)
* Anonymous logins - rare but worth a shot

```text
ssh 10.10.10.5
ssh anonymous@10.10.10.5
```

### SSH keys

When enumerating other services/shares, you should also look for SSH keys. Public keys are commonly stored as "authorized\_keys,", and private keys are commonly stored as "id\_rsa". If you locate a private key you may be able to connect  to the remote system via SSH.

```text
chmod 600 id_rsa
ssh -i id_rsa user@10.10.10.5
```

### Credential reuse

You should also attempt to connect to SSH with any credentials that you discover.

```text
ssh user@10.10.10.5
```

### Creating keys \(post exploitation\)

```text
ssh-keygen
```

### scp \(file transfers over ssh\)

```text
scp -r username@target-ip:/path/to/foo /home/username/desktop/
```

Specifying key exchange algorithms

Occasionally on older systems you'll receive and error indicating that no compatible key exchanges were found. Use the following command to force the use of a specific algorithm.

```text
ssh -o KexAlgorithms=diffie-hellman-group1-sha1 root@$TargetIP
```

