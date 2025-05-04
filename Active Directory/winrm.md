Open port (one of them):
- 5985/tcp
- 5986/tcp

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
