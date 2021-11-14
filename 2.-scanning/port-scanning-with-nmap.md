# Port Scanning with Nmap

Nmap is easily one of the most popular penetration testing tools.  While it started as a simple port scanner, the tool has grown immensely and is now performs multiple functions.  Knowing how to utilize Nmap's options to produce the desired level of detail in your scans is incredibly useful.  Below are  some example scan commands, as well as a list of the most commonly used options.

#### My preferred scans

```
Quick/standard scan: nmap -sC -sV 10.11.1.5
Deep scan: nmap -p- -sC -sV 10.11.1.5
UDP scan: nmap -sU -F 10.11.1.5
```

#### Scan types

```
-sT = TCP connect scan
-sS = TCP SYN (stealth) scan
-sU = UDP scan
-sn = host discovery only (no port scan)
-sN = null scann (no flags set, may help on firewalled systems)
-sX = Xmas tree scan (FIN, PSH, URG flags)
```

#### Other important flags

```
-sC = runs default scripts
-sV = attempts to identify the version of the service running on a port
-O = attempts OS detection using TCP/IP fingerprinting
-A = includes -sC, -sV, -O
-p = used to specify ports
-p- = scans all ports, not just top 1,000 default ports
--top-ports=20 = will scan the top 20 ports, number can be specified 
-Pn = skip host discovery and scan all addresses
-T = enables timing options (0-5, default:3)
-v = increases the verbosity, nmap will print results while scan is in progress
```

#### Input list of hosts from file

```
-iL <filename> = scans list of IP addresses contained in a txt file
```

#### Outputting scan results&#x20;

```
-oN = outputs results in normal txt format
-oG = outputs results in greppable format
-oX = outputs results in XML format
-oS = outputs results in script kiddie format
-oA = outputs results in all formats
```
