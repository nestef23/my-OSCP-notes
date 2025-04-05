# Redis
Redis (/ˈrɛdɪs/;[7][8] Remote Dictionary Server)[7] is an in-memory key–value database, used as a distributed cache and message broker, with optional durability.[9]

## redis-cli
```
# Connect to Redis
redis-cli -h <IP>

## Execute following commands after connection
# information and statistics about the Redis server
INFO

# select database
SELECT <database number>
SELECT 0

# obtain all the keys in a database?
KEYS *

# Get value of key
# You will need to perform for each key a "type" command:
# > type <key>
# and depending on the response perform:
# for "string": get <key>
# for "hash": hgetall <key>
# for "list": lrange <key> 0 -1
# for "set": smembers <key>
# for "zset": zrange <key> 0 -1 withscores
GET FLAG
```
