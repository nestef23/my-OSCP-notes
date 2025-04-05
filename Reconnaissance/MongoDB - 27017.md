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
