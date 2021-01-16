# 53 - DNS

### Enumeration

### **nslookup**

```text
Follow these steps, in order
nslookup (starts the tool)
SERVER 10.10.10.13 (sets DNS server)
127.0.0.1 (queries local host)
10.13.13.13 (queries target)
```

### whois

```text
whois nintendo.com
whois 50.7.67.186
```

### host

```text
Host www.megacorpone.com (web server)
Host -t ns megacorpone.com (nameservers)
Host -t mx megacorpone.com (mail servers)
```

### Zone transfers

Next, attempt a zone transfer from the DNS server. If successful, this will can provide additional subdomains and/or other machines on the domain.

```text
dig axfr @10.10.10.10 Domain.com
host -l megacorpone.com ns1.megacorpone.com
```

###  Modify /etc/hosts or /etc/resolv.conf

Next, modify /etc/hosts to include the information discovered in the previous steps.  Alternatively, you can update /etc/resolv.conf to include the address of the DNS server--be sure to place the server on the top line so that it is queried before other entries.

```text
/etc/hosts entries
10.10.10.13    cronos.htb    www.cronos.htb    admin.cronos.htb
/etc/resolv.conf
nameserver    10.10.10.13 <--Place new entry on top!!
nameserver    8.8.8.8
```

### Automated tools

```text
dnsrecon -d megacorpone.com -t axfr
dnsenum zonetransferme.com
```

