## Intro
This is description of first steps to do when checking new machine

## Nmap
Use Nmap to discover open ports and services
```
nmap -sV -O -vv -T4 -p 1-50000 <IP>
# -sV - discover service names and versions
# -O - discover OS
# -vv - be more verbose
# -p 1-50000 - scan TCP ports 1 to 50000
# -T4 - scan faster

# Run Nmap safe scripts
nmap -sV -sc <IP>
```
Nmap offers great scripts for additional scanning of discovered services
```
# Find all scripts with ssh in the name
ls -alh /usr/share/nmap/scripts/*ssh*
```

### Additional sources
https://fareedfauzi.gitbook.io/oscp-playbook/port-scanning/nmap-scanning


