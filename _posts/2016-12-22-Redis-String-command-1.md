---
layout: post
title: Redis(String) 字符串命令集合
categories: Redis
description: Redis String命令集合 
keywords: Redis
---

字符串命令有一下几种：
- 
- Redis SET 命令、
- Redis Get 命令、
- Redis Getrange 命令、
- Redis Getset 命令、
- Redis Getbit 命令、
- Redis Mget 命令、
- Redis Setbit 命令、
- Redis Setex 命令、
- Redis Setnx 命令、
- Redis Setrange 命令、
- Redis Strlen 命令、
- Redis Mset 命令、
- Redis Msetnx 命令、
- Redis Psetex 命令、
- Redis Incr 命令、
- Redis Incrby 命令、
- Redis Incrbyfloat 命令、
- Redis Decr 命令、
- Redis Decrby 命令、
- Redis Append 命令

<!--more-->

# Redis SET 命令 - 设置指定 key 的值

Redis SET 命令用于设置给定 key 的值。如果 key 已经存储其他值， SET 就覆写旧值，且无视类型。

**语法**

redis SET 命令基本语法如下：

```java
redis 127.0.0.1:6379> SET KEY_NAME VALUE
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

在 Redis 2.6.12 以前版本， SET 命令总是返回 OK 。

从 Redis 2.6.12 版本开始， SET 在设置操作成功完成时，才返回 OK 。

**实例**

首先，我们在 redis 中创建一个 key 并设置值。

```java
# 对不存在的键进行设置
 
redis 127.0.0.1:6379> SET key "value"
OK
 
redis 127.0.0.1:6379> GET key
"value"
 
 
# 对已存在的键进行设置
 
redis 127.0.0.1:6379> SET key "new-value"
OK
 
redis 127.0.0.1:6379> GET key
"new-value"
```

----------

# Redis Get 命令 - 获取指定 key 的值。

Redis Get 命令用于获取指定 key 的值。如果 key 不存在，返回 nil 。如果key 储存的值不是字符串类型，返回一个错误。

**语法**

redis Get 命令基本语法如下：

```java
redis 127.0.0.1:6379> GET KEY_NAME
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

返回 key 的值，如果 key 不存在时，返回 nil。 如果 key 不是字符串类型，那么返回一个错误。

**实例**

```java
# 对不存在的 key 或字符串类型 key 进行 GET
 
redis> GET db
(nil)
 
redis> SET db redis
OK
 
redis> GET db
"redis"
 
 
# 对不是字符串类型的 key 进行 GET
 
redis> DEL db
(integer) 1
 
redis> LPUSH db redis mongodb mysql
(integer) 3
 
redis> GET db
(error) ERR Operation against a key holding the wrong kind of value
```

----------

# Redis Getrange 命令 - 返回 key 中字符串值的子字符

Redis Getrange 命令用于获取存储在指定 key 中字符串的子字符串。字符串的截取范围由 start 和 end 两个偏移量决定(包括 start 和 end 在内)。

**语法**

redis Getrange 命令基本语法如下：

```java
redis 127.0.0.1:6379> GETRANGE KEY_NAME start end
```

**可用版本**

```java
>= 2.4.0
```

**返回值**

截取得到的子字符串。

**实例**

首先，设置 mykey 的值并截取字符串。

```java
redis 127.0.0.1:6379> SET mykey "This is my test key"
OK
redis 127.0.0.1:6379> GETRANGE mykey 0 3
"This"
redis 127.0.0.1:6379> GETRANGE mykey 0 -1
"This is my test key"
```

----------

# Redis Getset 命令 - 将给定 key 的值设为 value ，并返回 key 的旧值(old value)。

Redis Getset 命令用于设置指定 key 的值，并返回 key 旧的值。

**语法**

redis Getset 命令基本语法如下：

```java
redis 127.0.0.1:6379> GETSET KEY_NAME VALUE
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

返回给定 key 的旧值。 当 key 没有旧值时，即 key 不存在时，返回 nil 。

当 key 存在但不是字符串类型时，返回一个错误。

**实例**

首先，设置 mykey 的值并截取字符串。

```java
redis 127.0.0.1:6379> GETSET mynewkey "This is my test key"
(nil)
redis 127.0.0.1:6379> GETSET mynewkey "This is my new value to test getset"
"This is my test key"
```

----------

# Redis Getbit 命令 - 对 key 所储存的字符串值，获取指定偏移量上的位(bit)。

Redis Getbit 命令用于对 key 所储存的字符串值，获取指定偏移量上的位(bit)。

**语法**

redis Getbit 命令基本语法如下：

```java
redis 127.0.0.1:6379> GETBIT KEY_NAME OFFSET
```

**可用版本**

```java
>= 2.2.0
```

**返回值**

字符串值指定偏移量上的位(bit)。

当偏移量 OFFSET 比字符串值的长度大，或者 key 不存在时，返回 0 。

**实例**

```java
# 对不存在的 key 或者不存在的 offset 进行 GETBIT， 返回 0
 
redis> EXISTS bit
(integer) 0
 
redis> GETBIT bit 10086
(integer) 0
 
 
# 对已存在的 offset 进行 GETBIT
 
redis> SETBIT bit 10086 1
(integer) 0
 
redis> GETBIT bit 10086
(integer) 1
```

----------

# Redis Mget 命令 - 获取所有(一个或多个)给定 key 的值。

Redis Mget 命令返回所有(一个或多个)给定 key 的值。 如果给定的 key 里面，有某个 key 不存在，那么这个 key 返回特殊值 nil 。

**语法**

redis Mget 命令基本语法如下：

```java
redis 127.0.0.1:6379> MGET KEY1 KEY2 .. KEYN
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

一个包含所有给定 key 的值的列表。

**实例**

```java
redis 127.0.0.1:6379> SET key1 "hello"
OK
redis 127.0.0.1:6379> SET key2 "world"
OK
redis 127.0.0.1:6379> MGET key1 key2 someOtherKey
1) "Hello"
2) "World"
3) (nil)
```

----------

# Redis Setbit 命令 - 对 key 所储存的字符串值，设置或清除指定偏移量上的位(bit)。

Redis Setbit 命令用于对 key 所储存的字符串值，设置或清除指定偏移量上的位(bit)。

**语法**

redis Setbit 命令基本语法如下：

```java
redis 127.0.0.1:6379> Setbit KEY_NAME OFFSET
```

**可用版本**

```java
>= 2.2.0
```

**返回值**

指定偏移量原来储存的位。

**实例**

```java
redis> SETBIT bit 10086 1
(integer) 0
 
redis> GETBIT bit 10086
(integer) 1
 
redis> GETBIT bit 100   # bit 默认被初始化为 0
(integer) 0
```


----------

# Redis Setex 命令 - 将值 value 关联到 key ，并将 key 的过期时间设为 seconds (以秒为单位)。

Redis Setex 命令为指定的 key 设置值及其过期时间。如果 key 已经存在， SETEX 命令将会替换旧的值。

**语法**

redis Setex 命令基本语法如下：

```java
redis 127.0.0.1:6379> SETEX KEY_NAME TIMEOUT VALUE
```

**可用版本**

```java
>= 2.0.0
```

**返回值**

设置成功时返回 OK 。

**实例**

```java
redis 127.0.0.1:6379> SETEX mykey 60 redis
OK
redis 127.0.0.1:6379> TTL mykey
60
redis 127.0.0.1:6379> GET mykey
"redis
```

----------

# Redis Setnx 命令 - 只有在 key 不存在时设置 key 的值。

Redis Setnx（SET if Not eXists） 命令在指定的 key 不存在时，为 key 设置指定的值。

**语法**

redis Setnx 命令基本语法如下：

```java
redis 127.0.0.1:6379> SETNX KEY_NAME VALUE
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

设置成功，返回 1 。 设置失败，返回 0 。

**实例**

```java
redis> EXISTS job                # job 不存在
(integer) 0
 
redis> SETNX job "programmer"    # job 设置成功
(integer) 1
 
redis> SETNX job "code-farmer"   # 尝试覆盖 job ，失败
(integer) 0
 
redis> GET job                   # 没有被覆盖
"programmer"
```

----------

# Redis Setrange 命令 - 用 value 参数覆写给定 key 所储存的字符串值，从偏移量 offset 开始。

Redis Setrange 命令用指定的字符串覆盖给定 key 所储存的字符串值，覆盖的位置从偏移量 offset 开始。

**语法**

redis Setrange 命令基本语法如下：

```java
redis 127.0.0.1:6379> SETRANGE KEY_NAME OFFSET VALUE
```

**可用版本**

```java
>= 2.2.0
```

**返回**

被修改后的字符串长度。

**实例**

```java
redis 127.0.0.1:6379> SET key1 "Hello World"
OK
redis 127.0.0.1:6379> SETRANGE key1 6 "Redis"
(integer) 11
redis 127.0.0.1:6379> GET key1
"Hello Redis"
```

----------

# Redis Strlen 命令 - 返回 key 所储存的字符串值的长度。

Redis Strlen 命令用于获取指定 key 所储存的字符串值的长度。当 key 储存的不是字符串值时，返回一个错误。

**语法**

redis Strlen 命令基本语法如下：

```java
redis 127.0.0.1:6379> STRLEN KEY_NAME
```

**可用版本**

```java
>= 2.2.0
```

**返回值**

字符串值的长度。 当 key 不存在时，返回 0。

**实例**

```java
# 获取字符串的长度
 
redis> SET mykey "Hello world"
OK
 
redis> STRLEN mykey
(integer) 11
 
 
# 不存在的 key 长度为 0
 
redis> STRLEN nonexisting
(integer) 0
```

----------

# Redis Mset 命令 - 同时设置一个或多个 key-value 对。

Redis Mset 命令用于同时设置一个或多个 key-value 对。

**语法**

redis Mset 命令基本语法如下：

```java
redis 127.0.0.1:6379> MSET key1 value1 key2 value2 .. keyN valueN 
```

**可用版本**

```java
>= 1.0.1
```

**返回值**

总是返回 OK 。

**实例**

```java
redis 127.0.0.1:6379> MSET key1 "Hello" key2 "World"
OK
redis 127.0.0.1:6379> GET key1
"Hello"
redis 127.0.0.1:6379> GET key2
1) "World"
```

----------

# Redis Msetnx 命令 - 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。

Redis Msetnx 命令用于所有给定 key 都不存在时，同时设置一个或多个 key-value 对。

**语法**

redis Msetnx 命令基本语法如下：

```java
redis 127.0.0.1:6379> MSETNX key1 value1 key2 value2 .. keyN valueN 
```

**可用版本**

```java
>= 1.0.1
```

**返回值**

当所有 key 都成功设置，返回 1 。 如果所有给定 key 都设置失败(至少有一个 key 已经存在)，那么返回 0 。

**实例**

```java
# 对不存在的 key 进行 MSETNX
 
redis> MSETNX rmdbs "MySQL" nosql "MongoDB" key-value-store "redis"
(integer) 1
 
redis> MGET rmdbs nosql key-value-store
1) "MySQL"
2) "MongoDB"
3) "redis"
 
 
# MSET 的给定 key 当中有已存在的 key
 
redis> MSETNX rmdbs "Sqlite" language "python"  # rmdbs 键已经存在，操作失败
(integer) 0
 
redis> EXISTS language                          # 因为 MSET 是原子性操作，language 没有被设置
(integer) 0
 
redis> GET rmdbs                                # rmdbs 也没有被修改
"MySQL"
```

----------

# Redis Psetex 命令 - 这个命令和 SETEX 命令相似，但它以毫秒为单位设置 key 的生存时间，而不是像 SETEX 命令那样，以秒为单位。

Redis Psetex 命令以毫秒为单位设置 key 的生存时间。

**语法**

redis Psetex 命令基本语法如下：

```java
redis 127.0.0.1:6379> PSETEX key1 EXPIRY_IN_MILLISECONDS value1 
```

**可用版本**

```java
>= 2.6.0
```

**返回值**

设置成功时返回 OK 。

**实例**

```java
redis 127.0.0.1:6379> PSETEX mykey 1000 "Hello"
OK
redis 127.0.0.1:6379> PTTL mykey
999
redis 127.0.0.1:6379> GET mykey
1) "Hello"
```

----------

# Redis Incr 命令 - 将 key 中储存的数字值增一。

Redis Incr 命令将 key 中储存的数字值增一。

如果 key 不存在，那么 key 的值会先被初始化为 0 ，然后再执行 INCR 操作。

如果值包含错误的类型，或字符串类型的值不能表示为数字，那么返回一个错误。

本操作的值限制在 64 位(bit)有符号数字表示之内。

**语法**

redis Incr 命令基本语法如下：

```java
redis 127.0.0.1:6379> INCR KEY_NAME 
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

执行 INCR 命令之后 key 的值。

**实例**

```java
redis> SET page_view 20
OK
 
redis> INCR page_view
(integer) 21
 
redis> GET page_view    # 数字值在 Redis 中以字符串的形式保存
"21"
```

----------

# Redis Incrby 命令 - 将 key 所储存的值加上给定的增量值（increment） 。

Redis Incrby 命令将 key 中储存的数字加上指定的增量值。

如果 key 不存在，那么 key 的值会先被初始化为 0 ，然后再执行 INCRBY 命令。

如果值包含错误的类型，或字符串类型的值不能表示为数字，那么返回一个错误。

本操作的值限制在 64 位(bit)有符号数字表示之内。

**语法**

redis Incrby 命令基本语法如下：

```java
redis 127.0.0.1:6379> INCRBY KEY_NAME INCR_AMOUNT
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

加上指定的增量值之后， key 的值。

**实例**

```java
# key 存在且是数字值
 
redis> SET rank 50
OK
 
redis> INCRBY rank 20
(integer) 70
 
redis> GET rank
"70"
 
# key 不存在时
 
redis> EXISTS counter
(integer) 0
 
redis> INCRBY counter 30
(integer) 30
 
redis> GET counter
"30"
 
# key 不是数字值时
 
redis> SET book "long long ago..."
OK
 
redis> INCRBY book 200
(error) ERR value is not an integer or out of range
```


----------

# Redis Incrbyfloat 命令 - 将 key 所储存的值加上给定的浮点增量值（increment） 。

Redis Incrbyfloat 命令为 key 中所储存的值加上指定的浮点数增量值。

如果 key 不存在，那么 INCRBYFLOAT 会先将 key 的值设为 0 ，再执行加法操作。

**语法**

redis Incrbyfloat 命令基本语法如下：

```java
redis 127.0.0.1:6379> INCRBYFLOAT KEY_NAME INCR_AMOUNT
```

**可用版本**

```java
>= 2.6.0
```

**返回值**

执行命令之后 key 的值。

**实例**

```java
# 值和增量都不是指数符号
 
redis> SET mykey 10.50
OK
 
redis> INCRBYFLOAT mykey 0.1
"10.6"
 
# 值和增量都是指数符号
 
redis> SET mykey 314e-2
OK
 
redis> GET mykey                # 用 SET 设置的值可以是指数符号
"314e-2"
 
redis> INCRBYFLOAT mykey 0      # 但执行 INCRBYFLOAT 之后格式会被改成非指数符号
"3.14"
 
# 可以对整数类型执行
 
redis> SET mykey 3
OK
 
redis> INCRBYFLOAT mykey 1.1
"4.1"
 
# 后跟的 0 会被移除
 
redis> SET mykey 3.0
OK
 
redis> GET mykey                                    # SET 设置的值小数部分可以是 0
"3.0"
 
redis> INCRBYFLOAT mykey 1.000000000000000000000    # 但 INCRBYFLOAT 会将无用的 0 忽略掉，有需要的话，将浮点变为整数
"4"
 
redis> GET mykey
"4"
```

----------

# Redis Decr 命令 - 将 key 中储存的数字值减一。

Redis Decr 命令将 key 中储存的数字值减一。

如果 key 不存在，那么 key 的值会先被初始化为 0 ，然后再执行 DECR 操作。

如果值包含错误的类型，或字符串类型的值不能表示为数字，那么返回一个错误。

本操作的值限制在 64 位(bit)有符号数字表示之内。

**语法**

redis Decr 命令基本语法如下：

```java
redis 127.0.0.1:6379> DECR KEY_NAME 
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

执行命令之后 key 的值。

**实例**

```java
# 对存在的数字值 key 进行 DECR

redis> SET failure_times 10
OK

redis> DECR failure_times
(integer) 9

# 对不存在的 key 值进行 DECR
 
redis> EXISTS count
(integer) 0
 
redis> DECR count
(integer) -1

# 对存在但不是数值的 key 进行 DECR

redis> SET company YOUR_CODE_SUCKS.LLC
OK

redis> DECR company
(error) ERR value is not an integer or out of range
```

----------

# Redis Decrby 命令 - key 所储存的值减去给定的减量值（decrement） 。

Redis Decrby 命令将 key 所储存的值减去指定的减量值。

如果 key 不存在，那么 key 的值会先被初始化为 0 ，然后再执行 DECRBY 操作。

如果值包含错误的类型，或字符串类型的值不能表示为数字，那么返回一个错误。

本操作的值限制在 64 位(bit)有符号数字表示之内。

**语法**

redis Decrby 命令基本语法如下：

```java
redis 127.0.0.1:6379> DECRBY KEY_NAME DECREMENT_AMOUNT
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

减去指定减量值之后， key 的值。

**实例**

```java
# 对已存在的 key 进行 DECRBY
 
redis> SET count 100
OK
 
redis> DECRBY count 20
(integer) 80
 
 
# 对不存在的 key 进行DECRBY
 
redis> EXISTS pages
(integer) 0
 
redis> DECRBY pages 10
(integer) -10
```

----------

# Redis Append 命令 - 如果 key 已经存在并且是一个字符串， APPEND 命令将 value 追加到 key 原来的值的末尾。

Redis Append 命令用于为指定的 key 追加值。

如果 key 已经存在并且是一个字符串， APPEND 命令将 value 追加到 key 原来的值的末尾。

如果 key 不存在， APPEND 就简单地将给定 key 设为 value ，就像执行 SET key value 一样。

**语法**

redis Append 命令基本语法如下：

```java
redis 127.0.0.1:6379> APPEND KEY_NAME NEW_VALUE
```

**可用版本**

```java
>= 2.0.0
```

**返回值**

追加指定值之后， key 中字符串的长度。

**实例**

```java
# 对不存在的 key 执行 APPEND
 
redis> EXISTS myphone               # 确保 myphone 不存在
(integer) 0
 
redis> APPEND myphone "nokia"       # 对不存在的 key 进行 APPEND ，等同于 SET myphone "nokia"
(integer) 5                         # 字符长度
 
 
# 对已存在的字符串进行 APPEND
 
redis> APPEND myphone " - 1110"     # 长度从 5 个字符增加到 12 个字符
(integer) 12
 
redis> GET myphone
"nokia - 1110"
```
