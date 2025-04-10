##
File Transfer Protocol - old and hackable

## nc
We can use netcat to connect directly to the FTP and issue commands.
But it's not the best option.
```
nc <IP> 21
```

## ftp
Good old FTP client
```
ftp user@<IP>

# Sometimes anonymous user works without password
ftp anonymous@<IP>

# list contents
ls

# Download file
get <filename>
```

## ZIP cracking
If we manage to get a password-protected ZIP file we can use **John the ripper** to crack te password.
```
zip2john backup.zip > backup_hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt backup_hash.txt
```
