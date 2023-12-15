
## PowerView
https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1

Usage
```powershell
cd C:\<folder>
# will bypass the default policy for arbitrary PowerShell script execution.
powershell -ep bypass
# loads the PowerView script into the memory.
. .\PowerView.ps1 
```
### Find-InterestingDomainAcl
Usage
```powershell
# enumerate the privileges:
Find-InterestingDomainAcl -ResolveGuids

# Use filtering and select only interesting columns
Find-InterestingDomainAcl -ResolveGuids | Where-Object { $_.IdentityReferenceName -eq "hr" } | Select-Object IdentityReferenceName, ObjectDN, ActiveDirectoryRights
```
Intereting findings:
- `GenericWrite` permission can be used to compromise the account with that privilege by updating the `msDS-KeyCredentialLink` with a certificate. This vulnerability is known as the **Shadow Credentials attack**.
To exploit vulnerable user read `Shadow Credentials` from AD PrivEsc cheatsheet
