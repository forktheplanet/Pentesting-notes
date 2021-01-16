# 21 - FTP

FTP versions are typically fairly secure.  Check for anonymous login capability, if present enumerate whatever you have access to.

* Version info \(banner grab\)
* Anonymous logins - surprisingly common, especially in CTFs

```text
ftp 10.11.1.5
```

{% hint style="warning" %}
Remember to place FTP into the proper mode when transferring files \(binary for executable files and ASCII for text documents.  Use "binary" and "ascii" to change modes.
{% endhint %}

#### Basic Commands

FTP uses many basic Linux commands, below are the most common.

```text
ls - list directory contents
cd - change directory
get - copy file from remote to local
mget - copy multiple files from remote to local
put - copy file from local to remote
mput - copy multiple files from local to remote
delete - remove a file
pwd - print working directory on remote machine
bye/quit - exit ftp
```

#### Moving files

Some FTP servers \(ProFTPd\) are misconfigured and allow you to move files without authenticating.  If your enumeration uncovers file locations, you can use the commands below to try to move these files from inaccessible locations to areas you may have access to  \(smb shares, NFS, etc.\).

```text
SITE CPFR /path/to/file.txt
SITE CPTO /path/you/choose/file.txt
```

