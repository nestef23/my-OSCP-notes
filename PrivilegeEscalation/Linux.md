## Intro
Use Linpeas if possible

https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS

## Basic
Check if you can become root without password
```
su root
```

Check what priviliges you have (what can be run as sudo without password)

Compare with the list here: https://gtfobins.github.io/#+sudo

Also check which environment variables are inherited (look for the env_keep options)
```
sudo -l
```

## passwd and shadow

Check if you can read/write /etc/shadow.
- Can Write -> replace root password
- Can Read -> crack the passwords
```
ls -l /etc/shadow

# Generate new password hash to overwrite /etc/shadow
mkpasswd -m sha-512 test
```

Check if you can write to /etc/passwd
- Can write -> add root password directly here
```
ls -l /etc/passwd

# Generate new password hash to overwrite /etc/passwd
openssl passwd test
```

## Crontab
Check what is executed in cron
- edit the .sh files if possible
- replace executable files\
- check location of the PATH variable, can you do search order hijacking?
```
cat /etc/crontab
```

## SUID file
Executables that are executed in the context of root user.
Find all SUID files and look for the weird ones (e.g. in the user dir)

List of all commonly exploited SUID binaries: https://gtfobins.github.io/#+suid
```
find / -type f -perm -u=s 2>/dev/null
# or
find / -user root -perm -4000 -print 2>/dev/null
```

## Additional materials
https://book.hacktricks.xyz/linux-hardening/linux-privilege-escalation-checklist
