## lookupsid.py 
https://github.com/fortra/impacket/blob/master/examples/lookupsid.py
This tool will try brute forcing Windows Security Identifiers (SIDs) of any users in the AD domain.
Each user has a unique SID, which is comprised of their relative identifier (RID) concatenated with the domain SID. 
User SIDs are typically issued by a Domain Controller and are used in authorization and access mechanisms such as to form a part of the access token created during sign-in.
To enumerate the domain, we will specify the `guest` user, the domain name, and `-no-pass` for no password. 
```
impacket-lookupsid 'cicada.htb/guest'@cicada.htb -no-pass
```
