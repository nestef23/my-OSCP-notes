## psql
Connect to database
```
#psql -U christine -h localhost -p 5432
psql -U <user> -h <host> -p <port>
```
Do stuff
```
# In order to list the existing databases, we can execute the \l command, short for \list . 
\list

# Using the \c command, short for \connect , we can select a database and proceed to interact with its tables.
 \connect <database>

#  list the database's tables using the \dt command
\dt

# dump contents
SELECT * FROM <table>;
```
