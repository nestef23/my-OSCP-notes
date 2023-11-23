## Intro
Use Linpeas if possible

## Basic
Check if you can become root without password
```
su root
```
Check what priviliges you have
```
sudo -l
```


## SUID filed
Executables that are executed in the context of root user
Find all SUID files and look for the weird ones (e.g. in the user dir)
```
find / -type f -perm -u=s 2>/dev/null
# or
find / -user root -perm -4000 -print 2>/dev/null
```
