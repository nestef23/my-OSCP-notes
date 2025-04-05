# MySQL

## mysql
```
# Connect to database as root without password
mysql -u root -h <IP> -P 3306

# Connect with password
mysql -u <user> -p'<pass>' -h <IP> -P 3306

# select database
show databases;
use <database>;

# query info from tables
show tables;
select * from <tablename>;
```
