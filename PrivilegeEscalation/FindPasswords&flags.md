## Find user.txt and flag.txt
### Linux
```
# replace user.txt with root.txt as needed
find / -type f -name "user.txt" 2>/dev/null
find / -type f -name "user.txt" 2>/dev/null -exec cat {} \;
```
### Windows
```
dir C:\ /s /b user.txt 2>nul

Get-ChildItem -Path C:\ -Filter "user.txt" -Recurse -ErrorAction SilentlyContinue
```

## Find passwords in files
### Linux
```
# Example for the /var/www/html dir - searching from root (/) gives A LOT of results
find /var/www/html -type f -exec grep -iH "password" {} \; 2>/dev/null
```
### Windows
```
findstr /si /p "password" C:\*.* 2>nul

Select-String -Path "C:\**\*" -Pattern "password" -Context 2,2 -ErrorAction SilentlyContinue
```
