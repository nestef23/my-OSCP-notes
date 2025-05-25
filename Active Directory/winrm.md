Open port (one of them):
- 5985/tcp
- 5986/tcp

## netexec
Verify if user credentials work
```
netexec winrm <host/IP> -u <user> -p <password>
```

## evil-winrm
https://github.com/Hackplayers/evil-winrm

This shell is the ultimate WinRM shell for hacking/pentesting.
```
# Using password
evil-winrm -u <user> -p '<password>' -i <domain>

# Using NT hash
evil-winrm -u <user> -H '<NT hash>' -i <domain>

# Using cerificates
evil-winrm -k file.key -c file.crt -i <domain>

# Connect to encrypted winrm [5986/tcp]
evil-winrm -S
```
Menu with usefull functions
```
*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> menu
[+] Bypass-4MSI
[+] services
[+] upload
[+] download
[+] menu
[+] exit

```
Getting certs from PFX file: https://github.com/nestef23/my-OSCP-notes/blob/main/InitialAccess/SpecificCases/PFX_file.md
