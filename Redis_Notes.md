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

### Implementation note: 

Sorted sets are implemented via a dual-ported data structure containing both a skip list and a hash table.

Add: O(log(N))

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