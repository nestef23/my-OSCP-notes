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
