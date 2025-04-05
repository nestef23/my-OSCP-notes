# Rsync
```
# Enumerate shares /directories
rsync <IP>::

# List contents
rsync --list-only <IP>::
rsync <IP>::<name of directory>
rsync <IP>::path/to/smthing


# Download file
rsync <IP>::path/to/smthing/file.txt savedfilename.txt

# Download folder
rsync -r <IP>::path/to/smthing/
```

https://www.netspi.com/blog/technical-blog/network-pentesting/linux-hacking-case-studies-part-1-rsync/
