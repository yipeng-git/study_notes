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
    -   

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

