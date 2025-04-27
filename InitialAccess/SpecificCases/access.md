## .mdb files
The command "file backup.mdb" confirms that this is a Microsoft Access database.
```
└─$ file backup.mdb          
backup.mdb: Microsoft Access Database
```
which can be examined using **mdb-tools** (created by Brian Bruns). The tables are displayed with **mdb-tables**
and grep colour output is used to highlight tables of interest. 
```
└─$ mdb-tables backup.mdb          
acc_antiback acc_door acc_firstopen acc_firstopen_emp acc_holidays [...]
```
There is an **auth_user** table, in what seems to be a database backup from a **ZKAccess** installation. **ZKAccess** is an Access
Control software application, used to manage card readers and physical security of an environment.
Data from this table is exported using **mdb-export**, which reveals usernames and plaintext passwords.
```
└─$ mdb-export backup.mdb auth_user
id,username,password,Status,last_login,RoleID,Remark
25,"admin","admin",1,"08/23/18 21:11:47",26,
27,"engineer","access4u@security",1,"08/23/18 21:13:36",26,
28,"backup_admin","admin",1,"08/23/18 21:14:02",26,
```
