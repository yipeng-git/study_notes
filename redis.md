Bassicly a copy of Redis documentation + [【狂神说Java】Redis最新超详细版教程通俗易懂](https://www.bilibili.com/video/BV1S54y1R7SB)

-------

# 概述

https://redis.io/documentation

演进：

- 静态html -- 单机MySQL
- Memchached+MySQL+垂直拆分（读写分离）
    - 优化数据结构和索引->缓存文件->Memcached
- 分库分表+水平拆分+MySQL集群
    - MySQL早年用MyISAM引擎：表锁，高并发效率低
    - Innodb：行锁
    - 逐渐开始使用分库分表缓解写入压力
    - 推出集群

基本企业架构：

​	用户->企业防火墙/路由->负载均衡（主机/备用）->APP服务器（1,2,3..）->各种服务器（MySQL，缓存，移动信息服务器，Hadoop集群，实时通信服务器，流媒体服务器，图片服务器，文件服务器，群发服务器）

​	数据量爆发时增长，开始用NoSQL

​	Redis一秒写8万次，读11万次

​	An in-memory data structure server.

用途：

	1. 内存存储、持久化（rdb，aof）
	2. 效率高，可用于高速缓存
	3. 发布订阅系统
	4. 地图分析

特性：

1.  多样的数据类型
2.  持久化
3.  集群
4.  事务

# Redis Keys

**Size Limit = 512MB**

Redis keys are binary safe, this means that you can use any binary sequence as a key, from a string like "foo" to the content of a JPEG file. The empty string is also a valid key.

A few other rules about keys:

- Very long keys are not a good idea. For instance a  key of 1024 bytes is a bad idea not only memory-wise, but also because the lookup of the key in the dataset may require several costly key-comparisons. Even when the task at hand is to match the existence of a large value, hashing it (for example with SHA1) is a better idea, especially from the perspective of memory and bandwidth. **DON'T BE TOO LONG**
- Very short keys are often not a good idea. There is little Point in writing "u1000flw" as a key if you can instead write "user:1000:followers". The latter is more readable and the added space is minor compared to the space used by the key object it self and the value object. While short keys will obviously consume a bit less memory, your job is to find the right balance. **DON'T BE TOO SHORT EITHER**
- Try to stick with a schema. For instance `object-type:id` is a good idea, as in `user:1000`. **Dots** or **dashes** are ofen used for multi-word fields, as in `comment:1234:reply.to` or `comment:1234:reply-to`. **READABILITY**

## Redis key rules

1.  When we add an element to an aggregate data type, if the target key does not exist, an empty aggregate data type is created before adding the element.
2.  When we remove elements from an aggregate data type, if the value remains empty, the key is automatically destroyed. The **Stream data type is the only exception to this rule**.
3.  Calling a read-only command such as LLEN, or a write command removing elements, with an empty key, always produces the same result as if the key is holding an empty aggregate type of the type the command expects to find.

## Key Related Commands

https://redis.io/commands#generic

- `FLUSHALL` = Remove all keys from all databases
- `KEYS pattern` = Find all keys matching the given pattern
- `SET key value` = Set the string value of a key (replace any existing value already stored into the key)
- `EXISTS key` = Determine if a key exists
- `MOVE key db` = Move a key to another database
- `GET key` = Get the value of a key
- `EXPIRE key seconds` = Set a key's time to live in seconds
- `TTL key` = Get the time to live for a key
- `TYPE key` = Determine the type stored at key
- `APPEND key value` = Append a value to a key
- `DEL key` = Delete a key

# Data Types

https://redis.io/topics/data-types-intro

## String

The simplest type of value you can. associate with a Redis key. It is **the only data type** in Memcached.

### String Related Commands

https://redis.io/commands#string

- `STRLEN key` = Get the length of the value stored in a key.

- `APPEND key` value = Append a value to a key.

- `INCR key` = Increment the integer value of a key by one.

- `INCRBY key increment` = Increment the integer value of a key by the given amount.

- `INCRBYFLOAT key increment` = Increment the float value of a key by the given amount.

- `DECR key` = Decrement the integer value of a key by one.

- `DECRBY key decrement` = Decrement the integer value of a key by the given number.

- `GETRANGE key start end` = Get a substring of the string stored at a key. (**[START, END], `-1` = ENTIRE STRING**)

- `SETRANGE key offset value` = Overwrite part of a string at key **starting** at the specified offset.

- `SETEX key seconds value` = Set the calue and expiration of a key.

- `SETNX key value` = Set the value of a key, only if the key does not exist.

- `MSET key value [key value ...]` = Set multiple keys to multiple values.

    **This command can be used to insert multiple attributes like:**

    ```
    mset user:1:name zhangsan user:1:age 24
    ```

- `MSETNX key value [key value ...]` = Set mutiple keys to mutiple values, only if **none** of the keys exist 

- `GETSET key value` = Set the string value of a key and return its old value

-  `HSET key field value [field value]` = Set the string value of a hash field

    **Usage**:

    ```
    hset user:1 name zhangsan age 22 email zhangsan@email.com
    ```

## List

Redis lists are implemented via **Linked Lists**. This means that even if you have millions of elements inside a list, the operation of adding a new element in the head or the tail of the list is performed ***in constant time***. The speed of adding a new element with the `LPUSH` command to the head of a list with ten elements is the same as adding an element to the head of list with 10 million elements/

What's the down side? Accessing an element ***by index*** is not fast.

Redis LIsts are implemented with linked lists because for a database system it is crucial to be able to add elements to a very long list in a very fast way. Another strong advantage, as you'll see in a moment, is that Redis Lists can be taken at constant length in constant time.

When fast access to the middle of a large collection of elements is important, there is a different data structure that can be used, called sorted sets.

### List Related Commands

https://redis.io/commands#list

-   `LPUSH key element [element ...]` = Prepend one or mutiple elements to a list. **Return the length of the list after the push opt**

-   `LPUSHX key element [element ...]` = Prepend an element to a list, only if the list exists.

-   `LRANGE key start stop` = Get a range of elements from a list. (**[START, END], `-1` = ENTIRE STRING**)

-   `RPUSH key element [element ...]` = Append one or mutiple elements to a list.

-   `RPUSHX key element [element ...]` = Append an element to a list, only if the list exists.

-   `LPOP key [count]` = Remove and get the first elements in a list. 

-   `RPOP key [count]` = Remove and get the last elements in a list.

-   `LINDEX key index` = Get an element from a list by its index. **ZERO based list**

-   `LLEN key` = Get the length of a list

-   `LREM key count element` = Remove the first count occurence of elements from a list. **Return the num of elements removed**

    -   Count > 0: remove elements from head
    -   count < 0: remove elements from tail
    -   Count = 0: remove all elements

-   `LTRIM key start stop` = Trim an existing list so that it will contain onlyl the specified range of elements specified

    Common use:

    ```
    LPUSH mylist someelement
    LTRIM mylist 0 99
    # This pair of commands will push a new element on the list, while making sure that the list will not grow larger than 100 elements.
    ```

-   `RPOPLPUSH source destination` = Remove the last element in a list, prepend it to another list and return it.

-   `LSET key index element` = Set the list element at index to element. **An error is returned for out of range indexes**
-   `LINSERT key BEFORE|AFTER pivot element` = Insert an element before or after another element in a list. **Return -1 when the value pivot was not found**
-   `BRPOP key [key ...] timeout` = Remove and get the last element in a list, or block until one is aavailable. **Returns key value**

## Hash

Redis hashes look exactly how one might expect a "hash" to look, with field-value pairs.

No practice limits on the number of fields you can put inside a hash.

### Hash Related Commands

https://redis.io/commands#hash

-   `HSET key field value [field value]` = Set the string value of a hash field.
    -   As per Redis 4.0.0, HMSET is considered deprecated. Please prefer `HSET` in new code.
-   `HGET key field` = Get the value of a hash field.
-   `HMGET key field [field ...]` = Get the value of all the given hash fields.
-   `HGETALL key` = Get all the fields and values in a hash.
-   `HDEL key field [field ...]` = Delete one or more hash fields.
-   `HLEN key` = Get the number of fields in a hash.
-   `HEXISTS key field` = Determine if a hash field exists.
-   `HKEYS key` = Get all fields in a hash.
-   `HVALS key` = Get all the values in a hash.
-   `HINCRBY key field increment` = Increment the integer value of a hash field by the given number.
-   `HSETNX key field value` = Set the value of a hash field, only if the field does not exist.

### Common Usage of Redis Hashes

` hset user:1 name bob age 24`

## Set

Redis Sets are **unordered** collections of strings.

### Set Related Commands

https://redis.io/commands#set

-   `SADD key member [member ...]` = Add one or more members to a set.

-   `SMEMBERS key` = Get all the members in a set.

    Redis is free to return the elements in **ANY** order at every call.

-   `SISMEMBER key element` = Determine if a given value is a member of a set.

-   `SINTER key [key ...]` = Intersect multiple sets.

-   `SPOP key [count]` = Remove and return one or multiple random members from a set.

-   `SRANDMEMBER key [count]` = Get one or multiple random members from a set.

-   `SUNION key [key ...]` = Add mutiple sets.

-   `SUNIONSTORE destination key [key ...]` = Add multiple sets and **store** the resulting set in a key.

-   `SCARD key` = Get the number of members in a set.

-   `SMOVE source destination member` = Move a member from one set to another

-   `SDIFF key [key ...]` = Subtract multiple sets. **Return the members that only in the first set**

## Sorted Set

Sorted sets are a data type which is similar to a mix between a Set and a Hash. Like sets, sorted sets are composed of unique, non-repeating string elements, so in some sense a sorted set as a set as well.

However while elements inside sets are not ordered, every element in a sorted is associated with a floating point value, call *the score* (this is why the type is also similar to a hash, since every element is mapped to a value).

Moreover, elements in a sorted sets are *taken in order* (so they are not ordered on request, order is a peculiarity of the data structure used to represent sorted sets). They are ordered according to the following rule:

-   If A and B are two elements with a different score, then A > B if A.score is B.score.
-   If A and B have exactly the same score, then A > B if the A string is lexicographically greater than the B string. A and B strings can't be equal since sorted sets only have unique elements.

### Implementation note

Sorted sets are implemented via a dual-ported data structure containing both a skip list and a hash table.

Add: O(log(N))

### Sorted List

The average time complexity of search is O(logN), with normalized distributed level.

If use normalized distributed level, rebalance (O(N)) can be a problem after insertion (O(logN)). Thus when inserting a new element, we assign it a random number of level, and we only need to modify the pointers next to the new element.

```
randomlevel()
		level = 1;
		while random() < p and level < maxLevel do
				level + 1
    return level
```

Redis use `p = 1/4` and ''maxLevel = 32` as default.

### Why Redis uses skiplist

@antirez

```
There are a few reasons:

1) They are not very memory intensive. It’s up to you basically. Changing parameters about the probability of a node to have a given number of levels will make then less memory intensive than btrees.

2) A sorted set is often target of many ZRANGE or ZREVRANGE operations, that is, traversing the skip list as a linked list. With this operation the cache locality of skip lists is at least as good as with other kind of balanced trees.

3) They are simpler to implement, debug, and so forth. For instance thanks to the skip list simplicity I received a patch (already in Redis master) with augmented skip lists implementing ZRANK in O(log(N)). It required little changes to the code.
```



### Sorted Set Related Commands

-inf, +inf

-   `ZADD key score member [score member ...]` = Add one or more members to a sorted set, or update its score if already exists.
-   `ZCOUNT key min max` = Count the members in a sorted set with scores within the given values.
-   `ZCARD key` = Get the number of members in a sorted set.
-   `ZRANGEBYSCORE key min max` = Return a range of members in a sorted set, by score.
-   `ZRANGE key min max [BYSCORE|BYLEX] [WITHSCORES]` = Return a range of members in a sorted set.
    -   By index (rank).
-   `ZREM key member [member ...]` = Remove one or more members from a sorted set.
-   `ZREVRANGE key start stop` = Return a range of members in a sorted set, by index, with scores ordered from **high** to **low**.

## Bitmap

Bitmaps are not an actual data type, but a set of bit-orinted operations defined on the **String** type. Since strings are binary safe blobs and their maximum length is 512 MB, they are suitable to set up to 2^32 different bits.

Bit operations are divided into two groups: constant-time single bit operations, like setting a bit to 1 or 0, or getting its value, and operations on groups of bits, for example counting the number of set bits in a given range of bits (e.g., population counting).

One of the biggest advantages of bitmaps is that they often provide extreme space savings when storing information. For example in a system where different users are represented by incremental user IDs, it is possible to remember a single bit information (for example, knowing whether a user wants to receive a newsletter) of 4 billion of users using just 512 MB of memory.

### Bitmap Related Commands

Note: The string is grown to make sure it can hold a bit at *offset*. The *offset* is required to be within [0, 2^32].

-   `SETBIT key offset value` = Sets or clears the bit at offset in the string value stored at key.
-   `GETBIT key offset` = Returns the bit value at offset in the string value stored at key.
-   `BITCOUNT key [start end]` = Count set bits in a string.
-   `BITPOS key bit` = Find first bit set or clear in a string.

## HyperLogLog

A HyperLogLog is a probabilistic data structure used in order to count unique things (technically this is referred to estimating the cardinality of a set). Usually counting unique items requires using an amount of memory proportional to the number items you want to countk because you need to remember the elements you have already seen in the past in order to avoid counting them multiple items. However there is a set of algorithms that trade memory for precision: you end with an estimated measure with a standard error, which in the case of the Redis implementation is less than 1%. The magic of this algorithm is that you no longer need to use an amount of memory proportional to the number of items counted, and instead can use a constant amount of memory! 12k bytes in the worst case, or a lot less if you HyperLogLog has seen very few elements.

HLLs in Redis, while technically a different data structure, are encoded as a ** Redis string**, os you can call `GET` to serialize a HLL, and `SET` to deserialize it back to the server.

Conceptually the HLL API is like using Sets to do the same task. You would `SADD` every ovserved element into a set and would use `SCARD` to check the number of elements inside the set, which are uniue since `SADD` will not re-add an existing element.

While you don't really *add items* into an HLL, because the data structure only contains a state that does not include actual elements, the API is the same:

-   Every time you see a new element, you add it to the count with `PFADD`.
-   Every time you want to retrieve the current approximation of the unique elements *added* with `PFADD` so far, you use the `PFCOUNT`.

### HyperLogLog Related Commands

-   `PFADD key element [element ...]` = Adds the specified elements to the specified HyperLogLog.
-   `PFCOUNT key [key ...]` = Return the approximated cardinality of the set(s) ovserved by the HyperLogLog at key(s).
-   `PFMERGE destkey sourcekey [sourcekey ...]` = Merge N different HyperLogLogs into a single one.

## Geospatial

Redis has several commands related to geospatial indexing but unlike other commands these commands lack their own data type. These commands actually piggy back on the sorted set datatype. This is achieved by encoding the latitude and longitude into the score of the **sorted set** using the geohash algorithm.

**Can be operated with sorted set commands!**

### Geospatial Related Commands

-   `GEOADD key longitude latitude member [longtitude latitude member ...]` = Add one or more geospatial items in the geospatial index represented using a sorted set.
    -   Longitudes are from -180 to 180 degrees.
    -   Latitudes are from -85.05112878 to 85.05112878 degrees.
-   `GEOPOS key member [member ...]` = Returns longitude and latitude of members of a geospatial index.
-   `GEODIST key member1 member2 [m|km|ft|mi]` = Returns the distance between two members of a geospatial index.
-   `GEORADIUS key longitude latitude radius m|km|ft|mi` = Query a sorted set representing a geospatial index to fetch members matching a given maximum distance from a point.
-   `GEORADIUSBYMEMBER key member` = Query a sorted set representing a geospatial index to fetch members matching a given maximum distance from a member.
-   `GEOHASH key member [member ...]` = Returns members of a geospatial index as standard geohash strings.
-   `GEOSEARCH key` = uery a sorted set representing a geospatial index to fetch members inside an area of a box or a circle.

### Geohash String Properties

Geohash strings are 11 characters strings, no precision is loss compared to the Redis internal 52 bit representation.

-   They can be shortened removing characters from the right. It will lose precision but will still point to the same area.
-   It is possible to use them in `geohash.org` URLs such as `http://geohash.org/<geohash-string>/
-   Strings with a similar prefix are nearby, but the contrary is not true, it is possible that strings with different prefixes are nearby too.

# Redis Transactions

`MULTI`, `EXEC`, `DISCARD` and `WATCH` are the foundation of transactions in Reids. They allow the execution of a group of commands in a single step, with two important guarantees:

-   All the commands in a transaction are serialized and executed sequentially. It can **never** happen that a request issued by another client is served in the middle of the execution of a Redis transaction. This guarantees that the commands are executed as a single isolated operation. (**This *isolation* is different from the isolation in *relational databases*, commands are executed together after the `EXEC` command is triggered.**)
-   Either all of the commands or none are processed, so a Redis transaction is also **~~atomic~~** (***Atomicity* means *all occurs, or nothing occurs*. But Redis doesn't support roll-back on failure, and only guarantee the *execution* of commands**). The `EXEC` command triggers the **execution** of all the commands in the transaction, so if a client loses the connection to the server in the context of a transaction before calling the `EXEC` command none of the operations are performed, instead if the command is called, all the operations are performed. When using the `append-only file` Redis makes sure to use a single write(2) syscall to write the transaction on disk. However if the Redis server crashes or is killed by the system administrator in some hard way it is possible that only a partial number of operations are registered. Redis will detect this condition at restart, and will exit with an error. Using the `redis-check-aof` tool it is possible to fix the append only file that will remove the partial transaction so that the server can start again.

### Transaction Related Commands

-   `MULTI` = Mark the start of a transaction block.
-   `EXEC` = Execute all commands issued after `MULTI`.
-   `DISCARD` = Discard all commands issued after `MULTI`.
-   `WATCH key [key ...]` = Watch the given keys to determine execution of the `MULTI`/`EXEC` block.
-   `UNWATCH` = Forget about all watched keys.

### Errors inside a transaction

During a transaction it is possible to encounter two kind of command errors:

-   A command may fail to be queued, so there may be an error before `EXEC` is called. For instance the command may be syntatically wrong, or there may be some critical condition like an out of memory condition.
-   A command may fail *after* `EXEC` is called, for instance since we performed an operation against a key with the wrong value (like calling a list operation against a string value).

Clients used to sense the first kind of errors, happening before the `EXEC` call, by checking the return value of the ueued command: if the command replies with QUEUED it was queued correctly, otherwise Redis returns an error. If there is an error while queueing a command, most clients will abort the transaction discarding it.

**However starting with Redis 2.6.5, the server will remember that there was an error during the accumulation of commands, and will refuse to execute the transaction returning also an error during `EXEC`, and discarding the transaction automatically.**

Before Redis 2.6.5 the behavior was to execute the transaction with just the subset of commands queued successfully in case the client called `EXEC` regardless of previous errors. The new behavior makes it much more simiple to mix transactions with pipelining, so that the whole transaction can be sent at once, reading all the replies later at once.

**Errors happening *after* `EXEC` instead are not handled in a special way: all the other commands will be executed even if some command fails during the transaction.**

It;s important to note that **even when a command fails, all the other commands in the queue are processed** - Redis will *not* stop the processing of commands.

### Why Redis does not support roll backs?

If you have relational databases background, the fact that Redis commands can fail during a transaction, but still Redis will execute the rest of the transaction instead of rolling back, may look odd to you.

However there are good opinions for this behavior:

-   Redis commands can fail only if called with a wrong syntax (and the problem is not detectable during the command queueing), or against keys holding the wrong data type: this means that in practical terms a failing command is the result of a programming errors, and a kind of error that is very likely to be detected during development,k and not in production.
-   Redis is internally simplified and faster because it does not need the ability to roll back.

An argument against Redis point of view is that bugs happen, however it should be noted that in general the roll back does not save you from programming errors. For instance if a query increments a key by 2 instead of 1, or increments the wrong key, there is no way for a rollback mechanism to help. Given that no one can save the programmer from his or her errors, and that the kind of errors required for a Redis command to fail are unlikely to enter in production, we select the simpler and faster approach of not supporting roll backs on errors.

### Optimistic Locking Using Check-and-Set

`WATCH` is used to provide a check-and-set (CAS) behavior to Redis transactions.

**WATCHed** keys are monitored in order to detect changes against them. If at least one watched key is modified before the `EXEC` command, the whole transaction abords, and `EXEC` returns a **Null reply** to notify that the transaction failed.

This will work reliably only if we have a single client performing the operation in a given time. If multiple clients try to increment the key at about the same time there will be a race condition. For instance, client A and B will read the old value, for instance, 10. The value will be incremented to 11 by both the clients, and finally `SET` as the value of the key. So the final value will be 11 instead of 12.

Thanks to `WATCH` we are able to model the problem very well:

```
WATCH mykey
val = GET mykey
val = val + 1
MULTI
SET MYKEY $val
EXEC
```

Using the above code, if there are race conditions and another client modifies the result of val in the time between our call to `WATCH` and our call to `EXEC`, the transaction will fill.

We just have to repeat the operation hoping this time we'll not get a new race. This forms of locking is called *optimistic locking* and is very powerful form of locking. In many use cases, mutiple clients will bge accessing different keys, so collisions are unlikely - usually there's no need to repeat the operation.



### WATCH Explained

So what is `WATCH` really about? It is a command that iwll make the `EXEC` conditional: we are asking Redis to perform the transaction only if none of the **WATCH**ed keys were modified. (But they might be changed by the same sliend inside the transaction without aborting it.) Otherwise the transaction is not entered at all. (Note that if you `WATCH` a volatile key and Redis expires the key after you **WATCH**ed it, `EXEC` will still work.)

`WATCH` can be called multiple times. Simply all the `WATCH` calls will have the effect to watch for changes starting from the call, up to the moment `EXEC` is called. You can also send any number of keys to a single `WATCH` call.

When `EXEC` is called, all keys are **UNWATCH**ed, regardless of whether the transaction was aborted or not. Also when a cliend connection is closed, everything get **UNWATCH**ed.

It is also possible to use the `UNWATCH` command (without arguments) in order to flush all the watched keys. Sometimes this is useful as we optimistically lock a few keys, since possibly we need to perform a transaction to alter those keys, but after reading the current content of the keys we don't want to procced. When this happens we just call `UNWATCH` so that the connection can already be used freely for new transactions.

### Using `WATCH` to Implement `ZPOP`

A good example to illustrate how `WATCH` can be used to create new atomic operations otherwise not supported by Redis is to implement `ZPOP`, that is a command that pops the element with the lower score from a sorted set in an atomic way. This is the simplest implementation:

```
WATCH zset
element = ZRANGE zset 0 0
MULTI
ZREM zset element
EXEC
```

If `EXEC` fails we just repeat the operation.

### Redis Scripting and Transactions

A Redis script is transactional by defination, so everything you can do with a Redis transaction, you can also do with a script, and usually the script will be both simpler and faster.

This duplication is due to the fact that scripting was introduced in Redis 2.6 while transactions already existed long before. However we are unlikely to remove the support for transactions in the short-term because it seems semantically opportune that even without resorting to Redis scripting it is still possible to avoid race conditions, especially since the implementation complexity of Redis transactions is minimal.

However it is not impossible that in a non immediate future we'll see that the whole user base is justi using scripts. If this happens we may deprecate and finally remove transactions.

# Redis Configuration

## Passing argument via the command line

Since Redis 2.6 it is possible to also pass Redis configuration parameter using the command line directly. This is very useful for testing purposes.

```
./redis-server --port 6380 --slaveof 127.0.0.1 6379
```

The format of the arguments passed via the command line is exactly the same as the one used in the redis.conf file, with the exception that the keyword is prefixed with --.

Note that internally this generates an in-memory temporary config file (possibly concatenating the config file passed by the user if any) where arguments are translated into the format of redis.conf.

## Changing Redis configuration while the server is running

Ig is possible to reconfigure Redis on the fly without stopping and restarting the service, or querying the current configuration programmatically using the special commands `CONFIG SET` and `CONFT GET`.

Not all the configuration directives are supported in this way, but most are supported as expected. Please refer to the documentation for more information.

Note that modifying the configuration on the fly **has no effects on the redis.conf file** so at the next restart of Redis the old configuration will be used instead.

Make sure to also modify the `redis.conf` file accordingly to the configuration you set using `CONFIG SET.` You can do it manually, or starting with Redis 2.8, you can just use `CONFIG REWRITE`, which will automatically scan your `redis.conf` file and update the fields which don't match the current configuration value. Fields non existing but set to the default value are not added. Comments inside your configuration file are retained.

## Configuring Redis as a cache

If you plan to use Redis just as a cache where every key will have an expireset, you may consider using the following configuration instead (assuming a max memory limit of 2 megabytes as example):

```
maxmemory 2mb
maxmemory-policy
```

## Units

-   1k => 1000 bytes
-   1kb => 1024 bytes
-   1m => 1000000 bytes
-   1mb => 1024*1024 bytes
-   1g => 1000000000 bytes
-   1gb => 1024\*1024\*1024 bytes

**Units are case insensitive so 1GB 1Gb 1gB are all the same.**

## Includes

Include one or more other config files. This is useful if you have a standard template that goes to all Redis servers but also need to customize a few per-server settings. Include files can include other files, so use this wisely.

Note option "indlude" won't be rewritten by command "CONFIG REWRITE" from admin or Redis Sentinel. Since Redis always uses the last processed line as a value of a configuration directive, you'd better put includes at the beginning of redis.conf file to avoid overwriting config change at runtime.

If instead you are interested in using includes to override configuration options, it is better to use include as the last line.

```
include /path/to/local.conf
```



## Network

### Bind addresses

By default, if no "bind" configuration directive is specified, Redis listens for connections from all the network interfaces available on the server. It is possible to listen to just one or multipl;e selected interfaces using the "bind" configuration directive, followed by one or more IP addresses.

If the computer running Redis is directly exposed to the internet, binding to all the interfaces is dangerous and will expose the instance to everybody on the internet.

```
bind 127.0.0.1 ::1
```

>   ::1 is the 127.0.0.1 in IPv6.

### Protected mode

Protected mode is a layer of security protection, in order to avoid that Redis instances left open on the internet are accessed and exploited.

When protected mode is on and if:

1.  The server is not binding explicity to a set of addresses using the "bind" directive.
2.  No password is configured.

The server only accepts connections from clients connecting from the IPv4 and IPv6 loopback addresses and ::1, and from Unix domain sockets.

By default protected mode is enabled. You should disable it only if you are sure you want clients from other hosts to connect to Redis even if no authentication is configured, nor a specific set of interfaces are explicitly listed using the "bind" directive.

```
protected-mode yes
```

### Ports

Accepting connections on the specified port, default is 6379. If port 0 is specified Redis will not listen on a TCP socket.

```
port 6379
```

### TCP listen() backlog

In high requests-per-second environments you need an high backlog in order to avoid slow clients connections issues. Note the Linux kernel will silently truncate it to the value of /proc/sys/net/core/somaxconn so make sure to raise both of the value of somaxconn and tcp_max_syn_backlog in order to get the desired effect.

```
tcp-backlog 511
```

### Unix socket

Specify the path for the Unix socket that will be used to listen for incoming connections. There is no default, so Redis will not listen on a unix socket when not specified.

``` 
# unixsocket /var/run/redis/redis.sock
# unixsocketperm 700
```

### Timeout

Close the connection after a client is idle for N seconds (0 to disable)

```
timeout 0
```

### TCP keepalive

If non-zero, use SO_KEEPALIVE to send TCP ACKs to clients in absence of communication. This is useful for two reasons:

1.  Detect dead peers.
2.  Take the connection alive from the point of view of network equipment in the middle.

On Linux, the specified value (in seconds) is the period used to send ACKs.
Note that to close the connection the double of the time is needed.
On other kernels the period depends on the kernel configuration.

A reasonable value for this option is 300 seconds, which is the new Redis default starting with Redis 3.2.1/

```
tcp-keepalive 300
```

## General

### Daemonize

By default Redis does not run as a deamon. Use 'yes' if you need it.
Note that Redis will write a pid file in /var/run/redis.pid when daemonized.

```
daemonize yes
```

### Pidfile

If a pid file is specified, Redis writes it where specified at startup and removes it at exit.

When the server runs non daemonized, no pid file is created if none is specified in the configuration. When the server is daemonized, the pid file is used even if not specified, defaulting to "/var/run/redis.pid".

Creating a pid file is best effort: if redis is not able to create it nothing bad happens, the server will start and run normally.

```
pidfile /var/run/redis/redis-server.pid
```

### Loglevel

Specify the server verbosity level. This can be one of:

-   debug (a lot of information, useful for development/testing)
-   verbose (many rarely useful info, but not a mess like the debug level)
-   notice (moderately verbose, what you want in production probably)
-   warning (only very important / critical messages are logged)

```
loglevel notice
```

### Number of databases

Set the number of databases. The default database is DB 0, you can select a different one on a per-connection basis using SELECT <dbid> where dbid is a number bettween 0 and 'databases'-1.

```
databases 16
```

## Snapshotting

### Save the DB on disk

Save <seconds> <changes>

Will save the DB if both the given number of seconds and the given number of write operations against the DB occurred.

In the example below the behaviour will be to save:

-   After 900 sec (15 min) if at least 1 key changed
-   After 300 sec (5 min) if at least 10 keys changed
-   After 60 sec if at least 10000 keys changed

Note: you can disable saving completly by commenting out all "save" lines.

It is also possible to remove all the previously configured save points by adding a save directive with only a single empty string argument like `save ""`

```
save 900 1
save 300 10
save 60 10000
```

### Stop on failure

By default Redis will stop accepting writes if RDB snapshots are enabled (at least one save point) and the latest background save failed. This will make the user aware (in a hard way) that data is not persisting on disk properly, otherwise chances are that no one will notice and some disaster will happen.

If the background saving process will start working again Redis will automatically allow writes again.

However if you have setup your proper monitoring of the Redis server and persistence, you may want to disable this feature so that Redis will continue to work as usual even if there are problem with disk, permisisons, and so forth.

```
stop-writes-on-bgsave-error yes
```

### Compression string objects

Compress string objects using LZF when dump .rdb databases? For default that's set to 'yes' as it's almost always a win. If you want to save some CPU in the saving child set it to 'no' but the dataset will likely be bigger if you have sompressible values or keys.

```
rdbcompression yes
```

###  Checksum

Since version 5 of RDB a CRC64 checksum is placed at the end of the file. This makes the format more resistant to corruption but there is a performance hit to pay (around 10%) when saving and loading RDB files, so you can disable it for maximum performances.

RDB files created with checksum disabled have a checksum of zero that will tell the loading code to skip the ckeck.

```
rdbchecksum yes
```

### Filename

The filename where to dump the DB.

```
dbfilename dump.db
```



### Working directory

The DB will be written inside this directory, with the filename specified above using the 'dbfilename' configuration directive.

The Append Only File will also be created inside this directory.

Note that you must specify a directory here, not a file name.

```
dir /var/lib/redis
```

## Replication

Master-Slave replication. TODO

## Security

Require clients to issue `AUTH <PASSWORD>` before processing any other commands. This might be useful in environments in which you do not trust others with access to the host running redid-server.

This should stay commented out for backword compatibility and because most people do not need auth (e.g. they run their own servers).

Warning: since Redis is pretty fast an outside user can try up to 150k passwords per second against a good box. This means that you should use a very strong password otherwise it will be very easy to break.

```
requirepass foobared
```

Or set password in command line:

```
config set requirepass 123456
```

## Limits

### Maxclients

Set the max number of connected clients at the same time. By default this limit is set 1000 clients, however if the Redis server is not able to configure the process file limit to allow for the specified limit the max number of allowed clients is set to the current file limit minus 32 (as Redis reserves a few file descriptors for internal uses).

```
# maxclients 10000
```

### Maxmemory

Don't use more memory than the specified amount of bytes. When the memory limit is reached Redis will try to remove keys according to the eviction policy selected (see maxmemory-policy).

If Redis can't remove keys according to the policy, or if the policy is set to 'noeviction', Redis will start to reply with errors to commands that would use more memory, like `SET`, `LPUSH`, and so on, and will continue to reply to read-only commands like `GET`.

This option is usually useful when using Redis as an LRU cache, or to set a hard memory limit for an instance (using the 'noeviction' policy).

WARNING: If you have slaves attached to an instance with maxmemory on, the size of the output buffers needed to feed the slaves are subtracted from the used memory count, so that network problems / resyncs will not trigger a loop where keys are evicted, and in turn the output buffer of slaves is full with DELs of keys evicted triggering the deletion of more keys, and so forth until the database is completely emptied.

In short... if you have slaves attached it is suggested that you set a lower limit for maxmemory so that there is some free RAM on the system for slave output buffers (but this is not neede if the policy is 'noeviction').

```
# maxmemory <bytes>
```

### Maxmemory policy

How Redis will select what to remove when maxmemory is reached. You can select among five behaviors:

-   volatile-lru -> remove the key with an expire set using an LRU algorithm
-   allkeys-lru -> remove any key according to the LRU algorithm
-   volatile-random -> remove a random key with an expire set
-   allkeys-random ->remove a random key, any key
-   volatile-tll -> remove the key with the nearest expire time (minor TTL)
-   noeviction -> don't expire at all, just return an error on write operations

Note: with any of the above policies, Redis will return an error on write operations, when there are no suitable keys for eviction. 
At the date of writing these commands are: `set setnx setex append incr decr rpush lpush rpushx lpushx linsert lset rpoplpush sadd sinter sinterstore sunion sunionstore sdiff sdiffstore zadd zincrby zunionstore zinterstore hset hsetnx hmset hincrby incrby decrby getset mset msetnx exec sort`

The default is:

```
# maxmemory-policy noeviction
```

LRU and mimnal TTL algorithms are not precise algorithms but approximated algorithms (in order to save memory), so you can tune it for speed or accuracy. For default Redis will check five keys and pick the one that was used less recently, you can change the sample size using the following configuration directive.

```
# maxmemory-samples 5
```

## Append Only Mode

### Appendonly

By default Redis asynchronously dumps the dataset on disk. This mode is good enough in many applications, but an issue with the redis process or a power outage may result into a few minutes of writes lost (depending on the configured save points).

The Append Only File is an alternative presistence mode that provides much better durability. For instance using the default data fsync policy (see later in the config file) Redis can lose just one second of writes in a dramatic event like a server power outage, or a single write if something wrong with the Redis process itself happends, but the operating systme is still running correctly.

AOF and RDB persistence can be enabled at the same time withou problems. If the AOF is enabled on startup Redis will load the AOF, that is the file with the better durablity guarantees.

Please check http://redis.io/topics/persistence for more information.

```
appendonly no
```

### Filename

The name of the append only file (default: "appendonly.aof").

```
appendfilename "appendonly.aof"
```

### fsync()

The fsync() call tells the Operating System to actually write data on disk instead of waiting for more data in the output buffer. Some OS will really flush data on disk, some other OS will just try to do it ASAP.

Redis supports three different modes:

-   no: don't fsync, just let the OS flush the data when it wants. Faster. 
-   always: fsync after every write to the append only log. Slow, Safest.
-   everysec: fsync only one time every second. Compromise.

The default is "everysec", as that's usually the right compromise between speed and data safety. It's up to you to understand if you can relax this "no" that will let the operating system flush the output buffer when it wants, for better performances (but if you can live with the ida of some data loss consider the dafault persistence mode that's snapshotting), or on the contrary, use "always" that's very slow but a bit safer than everysec.

More details please check the following article:
http://antirez.com/post/redis-persistence-demystified.html

If unsure, use "everysec".

```
# appendfsync always
appendfsync everysec
# appendfsync no
```

TODO

## LUA Scripting

## Redis Cluster

## Slow Log

## Latency Monitor

## Event Notification

## Advanced Config

# Redis Persistence

Redis provides a different range of persistence options:

-   **RDB** (Redis Database): The RDB persistence performs point-in-time snapshots of your dataset at specified intervals.
-   **AOF** (Append Only File): The AOF persistence logs every write operation received by the server, that will be played again at server startup, reconstructing the original dataset. Commands are logged using the same format as the Redis protocol itself, in an append-only fashion. Redis is able to rewrite the log in the background when it gets too big.
-   **No persistence**: If you wish, you can disable persistence completely, if you want your data to just exist as long as the server is running.
-   **RDB + AOF**: It is possible to combine both AOF and RDB in the same instance. Notice that, in this case, when Redis restarts the AOF file will be used to reconstruct the original dataset since it isguaranteed to be the most complete.

The most important thing to understand is the different trade-offs between the RDB and AOF persistence. Let's start with RDB:

## RDB advantages

-   RDB is a very compact single-file point-in-time representation of your Redis data. RDB files are perfect for backups. For instance you may want to archive your RDB files every hour for the latest 24 hours, and to save an RDB snapshot every day for 30 days. This allows you to easily restore different versions of the data set in case of disasters.
-   RDB is very good for disater recovery, being a single compact file that can be transferred to far data centers, or onto Amazon S3 (possibly encrypted).
-   RDB maximize Redis performances since the only work the Redis parent process needs to do in order to persist is forking a child that will do all the rest. The parent instance will never perform disk I/O or alike.
-   RDB allows faster restarts with big datasets compared to AOF.
-   On replicas, RDB supports partial resynchronizations after restarts and failovers.

## RDB disadvantages

-   RDB is NOT good if you need to minize the chanceof data loss incase Redis stops working (for example after a power outage). You can configure different **save points** where an RDB is produced (for instance after at least five minutes and 100 writes against the data set, but you can have multiple save points). However you'll usually create an RDB snapshot every five minutes or more, so in case of Redis stopping working without a correct shutdown for any reason you should be prepared to loss the latest minutes of data.
-   RDB needs to `fork()` often in order to persist on disk using a child process. `Fork()` can be time cosuming if the dataset is big, and may result in Redis to stop serving clients for some millisecond or even for one second if the dataset is very big and the CPU performance not great. AOF also needs to `fork()` but you can tune how often you want to rewrite your logs without any trade-off on durability.

## AOF advantages

-   Using AOF Redis is much more durable: you can have different fsync policies: no fysnc at all, fysnc every second, fysnc at every query. With the default policy of fsync every second write performances are still great (fsync is performed using a background thread and the main thread will try hard to perform writes when no fsync is in progress.) but you can only loss one second worth of writes.
-   The AOF log is an append only log, so there are no seeks, nor corruption problems if there is power outage. Even if the log ends with an half-written command for some reason (disk full or other reasons) the refis-check-aof toll is able to fix it easily.
-   Redis is able to sutomatically rewrite the AOF  in background when it gets too big. The rewrite is completely safe as while Redis continues appending to the old file, a completely new one is produced with the minimal set of operations needed to create the current data set, and once this second file is ready Redis switches the two and starts appending to the new one.
-   AOF contains a log of all the operations one after the other in an easy to understand and parse format. You can even easily export an AOF file. For instance even if you've accidentally flushed everything using the `FLUSHALL` command, as long as no rewrite of the log was performed in the meantime, you can sitll save your data set just by stopping the server, removing the latest command, and restart Redis again.

## AOF disadvantages

-   AOF files are usually bigger than the equivalent RDB files for the same dataset.
-   AOF can be slower than RDB depending on the exact fsync policy. In general with fysnc set to *every second* performance is still very high, and with fsync disabled it should be exactly as fast as RDB even under high load. Still RDB is able to provide more guarantees about the maximum latency even in the case of a huge write load.
-   In the past we experienced rara bugs in specific commands (forinstance there was one involving blocking commands like `BRPOPLPUSH`) causing the AOF produced to not reproduce exactly the same dataset on reloading. These bugs are rare and we have tests in the test suite creating random complex datasets automatically and reloading them to check everything is fine. However, these kind of bugs are almost impossible with RDB persistence. To make this point clear: the Redis AOF works by increamentally updating an existing state, like MySQL or MongoDB does, while the RDB snapshotting creats everything from scratch again and again, that is conceptually more robust. However - 1) It should be noted that every time the AOF is rewritten by Redis it is recreated from scratch starting from the actual data contained in the data set, making resistance to bugs stronger compared to an always appending AOF file (or one rewritten reading the old AOF instead of reading the data in memory). 2) We have never had a single report from users about an AOF corruption that was detected in the real world.

## Ok, so what should I use?

The general indication is that you should use both persistence methods if you want a degree of data safety comparable to what PostgreSQL can provide you.

If you care a lot about your data, but still can live with a few minutes of data loss in case of disasters, you can simply use RDB alone.

There are many users using AOF alone, but we discourage it since to have an RDB snapshot from time to time is a great idea for doing database backups, for faster restarts, and in the event of bugs in the AOF engine.

Note: for all these reasons we'll likely end up unifying AOF and RDB into a single persistence mode in the future (long temr plan).

The following sections will illustrate a few more details about the two persistence models.

## Snapshotting

By default Redis saves snapshots of the dataset on disk, in a binary file called `dump.rdb`. You can configure Redis to have it save the dataset every N seconds if there are at least M changes in the dataset, or you can manually call the `SAVE` or `BGSAVE` commands.

This strategy is known as *snapshotting*.

### How it works

Whenever Redis needs to dump the dataset to disk, this is what happens:

-   Redis forks. We now have a child and a parent process. 
-   The child starts to write the dataset to a temporary RDB file.
-   When the child is done writing the new RDB file, it replaces the old one.

This method allows Redis to benefit from copy-on-write semantics.

## Append-only file

Snapshotting is not very durable. If your computer running Redis stops, your power line fails, or your accidentally `kill -9` your instance, the latest data written on Redis will get lost. While this may not be a big deal for some applications, there are use cases for fully durability, and in these cases Redis was not a viable option.

The *append-only file* is an alternative, fully-durable strategy for Redis. It became available in version 1.1.

You can turn on the AOF in your configuration file: `appendonly yes`

From now on, every time Redis receives a command that changes the dataset (e.g. `SET`) it will append it to the AOF. When you restart Redis it will re-play the AOF to rebuild the dataset.

### Log rewriting

As you can guess, the AOF gets bigger and bigger as write operations are performed. For example, if you are incrementing a counter 100 times, you will end up with a single key in your dataset containing the final value, but 100 entries in your AOF. 99 of those entries are not needed to rebuild the current state.

So Redis supports an interesting feature: it is able to rebuild the AOF in background without interrupting service to clients. Whenever you issue a `BGREWRITEAOF` Redis will write the shortest sequence of commands needed to rebuild the current dataset in memory. If you're using the AOF with Redis 2.2 you will need to run `BGREWRITEAOF` from time to time. Redis 2.4 is able to trigger log rewriting automatically (see the 2.4 example configuration file for more information).

### How durable is the append only file?

You can configure how many times Redis will fsync data on disk. There are three options:

-   `appendfsync always`: `fsync` every time new commands are appended to the AOF. Very very slow, very safe. Note that the commands are appended to the AOF after a batch of commands from multiple clients or a pipeline are executed, so it means a single write and a single fysnc (before sending the replies).
-   `appendfsync every sec`: `fsync` every second. Fast enough in (2.4 likely to be as fast as snapshotting), and you can lose 1 second of data if there is a disaster.
-   `appendfsync no`: Never `fsync`, just put your data in the hands of the OS. The faster and less safe method. Normally Linux will flush data every 30 seconds with this configuration, but its up to the kernal exact tuning.

The suggested (and default) policy is to `fsync` every second. It is both very fast and pretty safe. The `always` policy is very slow in practice, but it supports group commit, so if there are mutiple parallel writes Redis will try to perform a single `fysnc` operation.

### What should I do if my AOF gets truncated?

It is possible that the server crashed while writing the AOF file, or that the volume where the AOF file is stored was full at the time of writing. When this happens the AOF still contains consistent data representing a given point-in-time version of the dataset (that may be old up to one second with the default AOF fsync policy), but the last command in the AOF could be truncated. The lastest major versions of Redis will be able to load the AOF anyway, just discarding the last non well formed command in the file. In this case the server will emit a log like the following:

```
* Reading RDB preamble from AOF file...
* Reading the remaining AOF tail...
# !!! Warning: short read while loading the AOF file !!!
# !!! Truncating the AOF at offset 439 !!!
# AOF loaded anyway because aof-load-truncated is enabled
```

You can change the default configuration to force Redis to stop in such cases if you want, but the default configuration is ocntinue regardless the fact the last command in the file is not well-formed, in order to guarantee availability after a restart.

Old versions of Redis may not recover, and may require the following steps:

-   Make a backup copy of your AOF file.

-   Fix the original file using the `redis-check-aof` tool that ships with Redis: 

    ```
    $ redis-check-aof --fix
    ```

-   Optionally use `diff -u` to check what is the difference between two files.

-   Restart the server with the fixed file.

### What should I do if my AOF gets corrupted?

The best thing to do is to run the `redis-check-aof` utility, initially without the `--fix` option, then understand the problem, jump at the given offset in the fie, and seee if it is possble to manually repair the file: the AOF uses the same format of the Redis protocol ans is quite simple to fix manually. Otherwise it is possible to let the utility fix the file for us, but in that cass all the AOF portion from the invalid part to the end of the file may be discarded, leading to a massive amount of data loss if the corruption happended to be the initial part of the file.

### How it works

Log rewriting uses the same copy-on-write trick already in use for snapshotting. This is how it works:

-   Redis forks, so now we have a child and a parent process.
-   The child starts writing the new AOF in a temporary file.
-   The parent accumulates all the new changes in a in-memory buffer (but at the same time it writes the new changes in the old append-only file, so if the rewriting fails, we are safe).
-   When the child is done rewriting the file, the parent gets a signal, and appends the in-memory buffer at the end of the file generaged by the child.
-   Profit! Now Redia atomically renames the old file into the new one, and starts appending new data into the new file.

## Interactions between AOF and RDB persistence

Redis >= 2.4 makes sure to avoid triggering an AOF rewrite when a RDB snapshotting operation is already in progress, or allowing a `BGSAVE` while the AOF rewrite is in progress. This prevents two Redis background processes from doing heavy disk I/O at the same time.

When snapshotting is in progress and the user explicitly requests a log rewrite operation using `BGREWRITEAOF` the server will reply with an OK status code telling the user the operation is scheduled, and the rewrite will start once the snapshotting is completed.

In the case both AOF and RDB persistence are enabled and Redis restarts the AOF file will be used to reconstruct the original dataset since it is guaranteed to be the most complete.

## Backing up Redis data

Before starting this section, makesure to read the following sentence: **Make Sure to Backup Your Database**. Disk break, instances in the cloud disappear, and so forth: no backups means huge risk of data disaappearing into /dev/null.

Redis is very data backup friendly since you can copy RDB files while the database is running: the RDB is never modified once produced, and while it gets produced it uses a temporary name and is renamed into this final destination atomically using rename(2) only when the new snapshot is complete.

This means that copying the RDB file is completely safe while the server is running. This is what we suggest:

-   Creating a cron job in your server creating hourly snapshots of the RDB file in one directory, and daily snapshot in a different directory.
-   Every time the cron scrpt runs, make sure to call the `find` command to make sure too old snapshots are deleted: for instance you can take hourly snapshots for the latest 48 hours, and daily snapshots for one or two months. Make sure to name the snapshots with data and time information.
-   At least one time every day make sure to transfer an RDB snapshot *outside your data center* or at least *outside the physical machine* running your Redis instance.

If you run a Redia instance with only AOF persistence enabled, you can still copy the AOF in order to create backups. The file may lack the final part but Redis will be still able to load it.

## Disaster recovery

Disaster recovery in the context of REdis is basically the same story as backups, plus the ability to transfer those backups in many different external data centers. T his way data is secured even in the case of some catastrophic event affecting the main data center where Redis is running and producing its snapshots.

Since many REdis users are in the startup scene and thus don't have plenty of money to spend we'll review the most interesting disaster recovery techniques that don't have too high costs.

-   Amazon S3 and other similar services are a good way for imppplementing your disaster recovery system. Simply transfer your daily or hourly RDB snapshot to S3 in an encrypted form. You can encrypt your data using `gpg -c` (in symmetric encryption mode). Make sure to store your password in many different safe places (for instance give a copy to the most important people of your organization). It is recommended to use multiple storage services for improved data safety.
-   Transfer your snapshot using SCP to far servers. This is a fairly simple and safe route: get a small VPS in a place that is very far from you, install ssh there, and generate an ssh client key without passphrase, then add it in the `authorized_keys` file of your small VPS. You are ready to transfer backups in an automated fashion. Get at least two VPS in two different providers for best results.

It is important to understand that this system can easily fail if not implemented in the right way. At least make absolutely sure that after the transfer is completed your are able to verify the file size (that should match the one of the file you copied) and possibly the SHA1 digest if you are using a VPS.

You also need some kind of independent alert system if the transfer of fresh backups is not working for some reason.

# Redis Protocol specification

Redis clients communicate with the REdis server using a protocol called **RESP**. RESP is a compromise between the following things:

-   Simple to implement.
-   Fast to parse.
-   Human readable.

## Networking layer

A clients connects to a REdis server creating a TCP connection to the port 6379.

## Request-REsponse model

Redis accepts commands composed of differetn arguments. Once a command is received, it is processed and a reply is sent back to the client. This is the simplest model possible, however there are two exceptions:

-   Reddis supports pipelining. So it is possible for clients to send mutiple commands at once, and wait for replies later.
-   When a Redis client subscribes to a Pub/Sub channel, the protocol changes semantics and becomes a *push* protocol, that is, the client no longer requires sending commands, because the server will automatically send to the client new messages as soon as they are received.

## RESP protocol description

RESP is actually a serialization protocol that supports the following data types: Simple Strings, Errors, Integers, Bulk Strings and Arrays.

The way RESP is used in Redis as a request-response protocol is the following:

-   Clients send commands to a Redis server as a RESP Array of Bulk Strings.
-   The server replies with one of the RESP types according to the command implementation.

In RESP, the type of some data depends on the first byte:

-   For **Simple Strings** the first byte of the reply is "+"
-   For **Errors** the first byte of the reply is "-"
-   For **Integers** the first byte of the reply is "."
-   For **Bulk Strings** the first byte of the reply is "$"
-   For **Arrays** the first byte of the reply is "*"

## RESP Simple Strings

Simple  Strings are a plus character, followed by a string that cannot contain a CR or LF, terminated by CRLF.

String "OK": `+OK\r\n`

## RESP Errors

`-Error message\r\n`

```
-ERR unknown command 'foobar'
-WRONGTYPE Operation against a key holding the wrong kind of value
```

## RESP Integers

`:100\r\n`

## RESP Bulk Strings

Bulk Strings are used in order to represent a single binary safe string up to 512 MB in length.

Bulk Strings are encoded in the following way:

-   A "$" byte folled by the number of bytes composing the string, terminated by CRLF.
-   The actual string data.
-   A final CRLF.

String "foobar":

```
$6\r\nfoobwr\r\n
```

An empty string:

```
$0\r\n\r\n
```

**Null Bulk STring**

```
$-1\r\n
```

## RESP Arrays

RESP Arrays format:

-   A * character as the first byte, followed by the number of elements in the array as a decimal number, folowed by CRLF.
-   An additional RESP type for every element of the Array.

An empty Array:

```
*0\r\n
```

An array of two RESP Bulk Strings "foo" and "bar":

```
*2\r\n$3\r\nfoo\r\n$3\r\nbar\r\n
```

Arrays can contains mixed types.

**Null Array**

```
*-1\r\n
```

## Null elements in Arrays

["foo",nil,"bar"]:

```
*3\r\n
$3\r\n
foo\r\n
$-1\r\n
$3\r\n
bar\r\n
```

## Sending commands to a Redis Server

**LLEN mylist**

```
C: *2\r\n
C: $4\r\n
C: LLEN\r\n
C: $6\r\n
C: mylist\r\n

S: :48293\r\n
```

## Multiple commands and pipelining

## Inline Commands

## High performance parser for the Redis protocol

```c
#include <stdio.h>

int main(void) {
    unsigned char *p = "$123\r\n";
    int len = 0;

    p++;
    while(*p != '\r') {
        len = (len*10)+(*p - '0');
        p++;
    }

    /* Now p points at '\r', and the len is in bulk_len. */
    printf("%d\n", len);
    return 0;
}
```

# Redis Pub/Sub

`SUBSCRIBE`, `UNSUBSCRIBE` and `PUBLISH` implement the Publish/Subscribe messaging paradigm where (citing Wikipedia) sender (publisher) are not programmed to send their messages to specific receivers (subscribers). Rather, published messages are characterized into channels, without knowledge of what (if any) subscribers there may be. Subscribers express interest in one or more channels, and only receive messages that are of interest, without knowledge of what (if any) publishers there are. This decouping of publishers and subscribers can allow for greater scalability and more dynamic network topology.

For instance in order to subscribe to channels `foo` and `bar` the client issues a `SUBSCRIBE` providing the names of the channels:

```
SUBSCRIBE foo bar
```

Messages sent by other clients to these channels will be pushed by Redis to all the subscribed clients.
A client subscribed to one or more channels should not issue commands, although it can subscribe and unsubscribe to and from other channels. The replies to subscription and unsubscription operations are sent in the form of messages, so that the client can just read a coherent stream of messages where the first element incicates the type of message. The commands that are allowed in the context of a subscribe client are `SUBSCRIBE`, `PSUBSCRIBE`, `UNSUBSCRIBE`, `PUNSUBSCRIBE`, `PINT` and `QUIT`.

Please note that `redis-cli` will not accept any commands once in subscribed mode and can only quit the mode with `Ctrl-C`.

## Format of pushed messages

A message is a Array reply with three elements.

The first element is the kind of the message:

-   `subscribe`: means that we successfully subscribed to the channel given as the second element in the reply. The third argument represents the number of channels we are currently subscribed to.
-   `unsubscribe`: means that we successfully unsubscribed from the channel given as second element in the reply. The third argument represnets the number of channels we are currently subscribed to. When the last argument is zero, we are no longer subscibed to any channel, and the client can issue any kind of Redis command as we are outside the Pub/Sub state.
-   `message`: it is a message received as a result of a `PUBLISH` command issued by another client. The second element is the name of the originating channel, and the third argument is the actual message payload.

## Database & Scoping

PubSub has no relation to the key space. It was made not interfere with it on any level, including database number.

Publishing on db 10, will be heard by a subscriber on db 1.

If you need scoping of some kind, prefix the channels with the name of environment (test, staging, production).

## Wire protocol exmaple

Subscribe channel first and channel second:

```
> SUBSCRIBE first second
```

The client receives

```
*3
$9
subscribe
$5
first
:1
*3
$9
subscribe
$6
second
:2
```

If another client issue a `PUBLISH` operation against the channel name second:

```
> PUBLISH second Hello
```

The subscriber receives:

```
*3
$7
message
$6
second
$5
Hello
```

Now the client unsubsscribes it self from all the channels usning the `UNSUBSCRIBE` command without additional arguments:

```
UNSUBSCRIBE
```

The client receives from the server:

```
*3
$11
unsubscribe
$6
second
:1
*3
$11
unsubscribe
$5
first
:0
```

## Pattern-matching subscriptions

```
PSUBSCRIBE news.*
```

## Messages matching both a pattern and a channel subscription

```
SUBSCRIBE foo
PSUBSCRIBE f*
```

## Redis Pub/Sub implementation

Redis-server use dictionary/map to maintain channels. The keys is are the channel names and the values are all subscribers as a list.

# Replication

At the base of Redis replication (excluding the high availability features provided as an additional layer by Redis Cluster or Redis Sentinel) there is a very simple to user and configure *leader follower* (master-slave) replication: it sllows replica Redis instances to be exact copies of master instances. The replica will automatically reconnect to the master every time the link breaks, and will attempt to be an exact copy of it *regardless* of what happens to the master.

This system works using three main mechanisms:

1.  When a master and a replica instances are well-connected, the master keeps the replica updated by sending a stream of commands to the replica, in order to replicate the effects on the dataset happening in the master side due to: client writes, keys expired or evicted, and any other action changing the master dataset.
2.  When the link between the master and the replica breaks, for network issues or because a timeout is sensed in the master or the replica, the replica reconnects and attempts to proceed with a partial resynchronization: it means that it will try to just botain the part of the stream of commands it missed during the disconnection.
3.  When a partial resynchronization is not possible, the replica will ask for a fun resynchronization. This will involve a more complex process in which the master needs to create a snapshot of all its data, send it to the replica, and then continue sending the stream of commands as the dataset changes.

Redis uses by default asynchronous replication, which being low latency and high performance, is the natural replication mode for the vast majority of Redis use cases. However, Redis replicas asynchronously acknowledge the amount of data they received periodically with the master. So the master does not wait every time for a command to be processed by the replicas, however, it knows, if needed, what replica already processed what command. This allows having optional synchronous replication.

Synchronous replication of certain data can be requested by the clients using the `WAIT` command. However `WAIT` is only able to ensure that there are the specified number of acknowledged copies in the other Redis instances, it does not turn a set of Redis instances into a CP system with strong consistency: acknowledged writes can still be lost during a failover, depending on the exact configuration of the Redis persistence. However with `WAIT` the probability of losing a write after a failure event is greatly reduced to certain hard to trigger failure modes.

Check Redis Sentinel and Redis cluster documentation for high availability.

Some very important facts about Redis replication:

-   Redis uses asynchronous replication, with asynchronous replica-to-master acknowledges of the amount of data processed.
-   A master can have multiple replicas.
-   Replicas are able to accept connections from other replicas. Aside from connecting a number of replicas to the same master, replicas can also be connected to other replicas in a cascading-like structure. Since Redis 4.0, all the sub-replicas will receive exactly the same replication stream from the master.
-   Redis replication is non-blocking on the master side. This means that the master will continue to handle queries when one or more replicas perform the initial synchronization or a partial resynchronization.
-   Replication is also largely non-blocking on the replica side. While the replica is performing the initial synchronization, iit can handle queries using the old version of the dataset, assuming you configured Redis to do so in redis.conf. Otherwise, you can configure Redis replicas to return an error to clients if the replication stream is down. However, after the initial sync, the old dataset must be deleted and the new one must be loaded. The replica will block incoming connection during this brief window (that can be as long as many seconds for every large datasets). Since Redis 4.0 it is possible to configure Redis so that the deletion of the old dataset happens in a different thread, however loading the new initial dataset will still happen in the main thread and block the replica.
-   Replication can be used both for scalability, in order to have multiple replicas for read-only queries, or simply for improving data safty and high availability.
-   It is possible to use replication to avoid the cost of having the master writing the full dataset to disk: a typical technique involves configuring your master `redis.conf` to avoid persisting to disk at all, then connect a replica configured to save from time to time, or with AOF enabled. However this set up must be handled with care, since a restarting master will start with an empty dataset: if the replica tries to asynchronize with it, the replica will be emptied as well.

## Safty of replication when master has persistenced turned off

**Avoid restarting automatically** after a reboot.

1.  We have a setup with node A acting as master, with persistence turned down, and nodes B and C replicating from A.
2.  Node A crashes, however it has some auto-restart system, that restarts the process. However since persistence is turned off, the node restarts with an empty dataset.
3.  Nodes B and C will replicate from node A, which is empty, so they'll effectively destroy their copy of data.

When Redis Sentinel is used for high availability, it is still dangerous to turn off persistence on the master. The master can restart fast enough for Sentinel to not detect a failure.

Auto restart of instances should be disabled when data safety is important and replication is used with master configured without persistence.

## How Redis replication works

Every Redis master has a replication ID: it is a large pseudo rendom string that marks a given story of the dataset. Each master also takes an offset that increments for every byte of replication stream that is produced to be sent to replicas, in order to update the state of the replicas with the new changes modifying the dataset. The replication offset is incremented even if no replica is actually connected, so b asically every given of: `Replication ID, offset` identifies an exact version of the dataset of a master.

When replicas connect to mastesrs, they use the `PSYNC` command in order to send their old master replication ID and the offsets they processed so far. This way the master can send just the incremental part needed. However if there is not enough *backlog* in the master buffers, or if the replica is referring to an history which is no longer known, then a full resynchronizaiton happens: in this case the replica will get a full copy of the dataset, from scratch.

This is how a full synchronizaiton works in more details:

The master starts a background saving process in order to produce an RDB file. At the same time it starts to buffer all new write commands received from the clients. When the background saving is complete, the master transfer the database file to the replica, which saves it on disk, and then loads it into memory. The master will then send all buffered commands to the replica. This is done as a stream of commands and is in the same. format of the Redis protocol it self.

## Diskless replication

Normally a full resynchronization requires creating an RDB file on disk, then reloading the same RDB from disk in order to feed the replicas with the data.

With slow disks this can be a very stressing operation for the master. Redis version 2.8.18 is the first version to have support for diskless replication. In this setup the child process directly sends the RDB over the wire to replicas, without using the disk as intermediate storage.

## Configuration

Just add `replicaof 192.168.1.1 6379` to the replica configuration file.

## Read-only replica

Since Redis 2.6, replicas support a read-only mode by adding `replica-read-only` in the redis conf file, and can be enabled and disabled at runtime using `CONFIG SET`.

Note that **writable replicas before version 4.0 were incapable of expiring keys with a time to live set**.

Also note that since Redis 4.0 replica writes are only local, and are not propagated to sub-replicas attached to the instance. Sub-replicas instead will always receive the replication stream identical to the one sent by the top-level master to the intermediate replicas.

## Allow writes only with N attached replicas

## How Redis replication deals with expires on keys

## Configuring replication in Docker and NAT

## The INFO and ROLE command

## Partial resynchronizations after restarts and failovers

Since Redis 4.0, when an instance is promoted to master after a failover, it wil be still able to perform a partial resynchronization with the replicas of the old master. To do so, the replica remembers the old replication and offset of its former master, so can provide part of backlkog to the connecting replicas even if they ask for the old replication.

However the new replication ID of the promoted replica will be different, since it consistutes a different history of the dataset. For example, the master can return available and can continue accepting writes for some time, so using the same replication ID in the promoted replica would violate the rule that a replication ID and offset pair identifies only a single data set.

Moreover, replicas - when powered off gently and restarted - are able to store in the `RDB` file the information needed in order to resynchronize with their master. This is useful in case of upgrades. When this is needed, it is better to user the `SHUTDOWN` command in order to perform a `save & quit` operation on the replia.

It is not possible to partially resynchronize a replica that restarted via the AOF file. However the instance may be turned to RDB persistence before sutting down it, than can be restarted, and finally AOF can be enabled again.

## Configure replicas

-   port
-   daemonize
-   pidfile
-   logfile
-   dbfilename dump.rdb
-   replicaof 192.168.1.1 6379
-   masterauth <password>
-   replica-read-only

# High Availability

## Redis Sentinel

Using Sentinel you can create a Redis deployment that resists withou human intervention certain kinds of failures. Redis Sentinel also provides other collateral tasks such as monitoring, notifications and acts as a configuration provider for clients.

The full list of Sentinel capabilities at a macroscopical level (i.e. the big picture):

-   **Monitoring**. Sentinel constantly checks if your master and replica instances are working as expected.
-   **Notification**. Sentinel can notify the system administrator, or other computer programs, via an API, tha something is wrong with one of the monitored Redis instances.
-   **Automatic failover**. If a master is not working as expected, Sentinel can start failover process wherer a replica is promoted to master, the other additional replicas are configured to use the new master, and the applications using the Redis server are informed about the new address to use when connecting.
-   **Configuration provider**. Sentinel acts as a source of authority for clients service directory: clients connect to Sentinels in order to ask for the address of the current Redis master responsible for a given service . If a failover occurs, Sentinels will report the new address.

### Distributed nature of Sentinel

Redis Sentinel is a distributed system:

Sentinel it self is designed to run in a configuration where there are mutiple Sentinel processes cooperating together. The advantage of having multiple Sentinel processes cooperating are the following:

1.  Failure detection is performed when multiple Sentinels agree about the fact a given master is no longer available. This lowers the probability of false positives.
2.  Sentinel works even if not all the Sentinel processes are working, making the system robust against failures. There is no fun in having a failover system which is itself a single point of failure, after all.

The sum of Sentinels, Redis instances and clients connecting to Sentinel and Redis, are also a large distributed system with specific properties. 

## Quick Start

### Obtaining Sentinel

The current version is called **Sentinel 2**, released since Redis 2.8. Redis Sentinel version 1, shipped with Redis 2.6, is deprecated and should not be used.

### Running Sentinel

You can start Sentinel it self as a executable or along with the `redis-server`.  Both ways work the same.

However **it is mandatory** to use a configuration file when running Sentinel, as this file will be used by the system in order to save the current state that will be reloaded in case of restarts. Sentinel wil simply refuse to start if no configuration file is given or if the configuration file path is not writable.

Sentinels by default run **listening for connections to TCP port 26379**, so for Sentinels to work, port 26379 of your servers **must be open** to receive connections from the IP addresses of the other Sentinel instances. Otherwise Sentinels can't talk and can't agree about what to do, so failover will never be performed.

### Fundamental things to know about Sentinel before deploying

1.  You need at least three Sentinel instances for a robust deployment.
2.  The three Senteinel instances should be placed into computers or virtual machines that are believed to fail in an independent way.
3.  Sentinel + Redis distributed system does not guarantee that acknowledged writes are retained during failures, since Redis uses asynchronous replication. However there are ways to deploy Sentinel that make the window to lose writes limited to certain moments, while there are other less secure ways to deploy it.
4.  You need Sentinel support in your clients. Popular client libraries have Sentinel support, but not all.
5.  There is no HA setup which is safe if you don't test from the time to time in development environments, or even b etter if you can, in production environments, if they work. You may have a misconfiguration that will become apparent only when it's too late (at 3am when you master stops working).
6.  **Sentinel, Docker, or other forms of Network Address Translation or Port Mapping should be mixed with care**: Docker performs port remapping, breaking Sentinel auto discovery of other Sentinel processes and the list of replicas of a master. Checkthe section about Sentinel and Docker later in this doc for more information.

### Configuring Sentinel

The Redis source distribution contains a file called `sentinel.conf` thst is a self-documented example configuration file you can use to configure Sentinel, however a typical minimal configuration file looks like the following:

```
sentinel monitor mymaster 127.0.0.1 6379 2
sentinel down-after-milliseconds mymaster 60000
sentinel failover-timeout mymaster 180000
sentinel parallel-syncs mymaster 1

sentinel monitor resque 192.168.1.3 6380 4
sentinel down-after-milliseconds resque 10000
sentinel failover-timeout resque 180000
sentinel parallel-syncs resque 5
```

You only need to specify the masters to monitor, giving each separated master a different name. There is no need to specify replicas, which are auto-discovered. Sentinel will update the configuration automatically with additional information about replicas. The configuration is alaso rewritten every time a replica is promoted to master during a failover and every time a new Sentinel is discovered.

The example above monitors two sets of Redis instances.

Sentinel monitor statement:

```
sentinel monitor <master-group-name> <ip> <port> <quorum>
```

About the **quorum** argument:

-   The **quorum** is the number of Sentinels that need to agree about the fact the master is not reachable, in order to really mark the master as failing, and eventually start a failover procedure if possible.
-   However **the quorum is only used to detect the failure**. In order to actually perform a failover, one of the Sentinels need to be elected leader for the failover and be authorized to proceed. This is only happens with the vote of the **majority of the Sentinel processes**.

In practical terms this means during failures **Sentinel never starts a failover if the majority of Sentinel processes are unable to talk**.

### Other Sentinel options

```
sentinel <option_name> <master_name> <option_value>
```

-   `down-after-milliseconds`
-   `parallel-syncs`

Configuration parameters can be modified at runtime:

-   Master-specific configuration parameters are modified using `SENTINEL SET`.
-   Global configuration parameters are modified using `SENTINEL CONFIG SET`.

### Example Sentinel deployments

## A quick tutorial

## Sentinel API

## More advanced concepts

## Algorithms and internals



# Latency Monitoring

# Security

# Redis Lua Scripting

# Memory Optimization

# Mass Insertion of data

# Cache Penetration and Cache Avalanche

