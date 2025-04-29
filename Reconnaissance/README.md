## Intro
This is description of first steps to do when checking new machine

## Nmap
Use Nmap to discover open ports and services
```
nmap -sV -sC -O -vv -T5 -p- <IP>
# -sV - discover service names and versions
# -sC - run safe scripts
# -O - discover OS
# -vv - be more verbose
# -p- scan ALL ports OR
# -p 1-50000 - scan TCP ports 1 to 50000
# -T5 - scan fastest
```
Nmap offers great scripts for additional scanning of discovered services
```
# Find all scripts with ssh in the name
ls -alh /usr/share/nmap/scripts/*ssh*
```
Basic vuln scan
```
nmap -Pn -T5 --script vuln <IP>
```

### Additional sources
https://fareedfauzi.gitbook.io/oscp-playbook/port-scanning/nmap-scanning


