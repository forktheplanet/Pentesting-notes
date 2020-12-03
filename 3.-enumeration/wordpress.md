# Wordpress

### Manual enumeration

* Enumerate users by reviewing the archives and taking note of authors of blog posts
* If you identify a login page, attempt to login with common credentials \(admin, password, etc.\).
  * Pay attention to errors produced through failed logins

### wpscan

wpscan is an open source scanner included with Kali.

If you use another distro you can download it here: [https://github.com/wpscanteam/wpscan](https://github.com/wpscanteam/wpscan)

Documentation here:  [https://github.com/wpscanteam/wpscan/wiki/WPScan-User-Documentation](https://github.com/wpscanteam/wpscan/wiki/WPScan-User-Documentation)

#### Enumerating users

```text
wpscan --url https://target.tld/ --enumerate u
wpscan --url example.com -e u
wpscan --url https://target.tld/ --enumerate u1-100
```

#### Brute force

```text
wpscan --url example.com -e u --passwords /path/to/password_file.txt
```

```text
wpscan --url example.com --passwords /usr/share/wordlists/rockyou.txt --usernames admin --max-threads 50
```

#### Scanning plugins

```text
wpscan --url example.com -e vp --plugins-detection mixed --api-token YOUR_TOKEN
```

#### Enumeration modes

To enumerate version, plugins or themes, select from three modes:  `passive, aggressive, mixed.`  The default is `mixed` for most items, and  `passive` for plugin detection.  To override the default use the`--plugins-detection` option.

```text
Mixed - provides the most results
Passive - useful when server overload is a concern
Aggressive - most aggressive
```

#### Other enumeration options

The following enumeration options are available and should be preceded by the `-e` flag.  If no additional options are provided the default is: `vp,vt,tt,cb,dbe,u,m`

* `vp` \(Vulnerable plugins\)
* `ap` \(All plugins\)
* `p` \(Popular plugins\)
* `vt` \(Vulnerable themes\)
* `at` \(All themes\)
* `t` \(Popular themes\)
* `tt` \(Timthumbs\)
* `cb` \(Config backups\)
* `dbe` \(Db exports\)
* `u` \(User IDs range. e.g: u1-5\)
* `m` \(Media IDs range. e.g m1-15

