---
layout: post
title: Redis键(key) 命令集合
categories: Redis
description: Redis Key命令集合 
keywords: Redis
---

# Redis DEL 命令 - 该命令用于在 key 存在是删除 key。

**Redis DEL 命令用于删除已存在的键。不存在的 key 会被忽略。**

## 语法

redis DEL 命令基本语法如下： 

```java
redis 127.0.0.1:6379> DEL KEY_NAME
```
<!--more-->
**可用版本**

```java
>= 1.0.0
```

**返回值**

被删除 key 的数量。

## 实例

首先，我们在 redis 中创建一个 key 并设置值。

```java
redis 127.0.0.1:6379> SET w3ckey redis
OK
```

现在我们删除已创建的 key。

```java
redis 127.0.0.1:6379> DEL w3ckey
(integer) 1
```

# Redis Dump 命令 - 序列化给定 key ，并返回被序列化的值。

**Redis DUMP 命令用于序列化给定 key ，并返回被序列化的值。**

## 语法

redis DUMP 命令基本语法如下：

```java
redis 127.0.0.1:6379> DUMP KEY_NAME
```

**可用版本**

```java 
>= 2.6.0
```

**返回值**

如果 key 不存在，那么返回 nil 。 否则，返回序列化之后的值。

## 实例

首先，我们在 redis 中创建一个 key 并设置值。

```java
redis> SET greeting "hello, dumping world!"
OK
```

现在使用 DUMP 序列化键值。

```java
redis> DUMP greeting
"\x00\x15hello, dumping world!\x06\x00E\xa0Z\x82\xd8r\xc1\xde"
 
redis> DUMP not-exists-key
(nil)
````

# Redis EXISTS 命令 - 检查给定 key 是否存在。

**Redis EXISTS 命令用于检查给定 key 是否存在。**

## 语法

redis EXISTS 命令基本语法如下：

```java
redis 127.0.0.1:6379> EXISTS KEY_NAME
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

若 key 存在返回 1 ，否则返回 0 。

## 实例

```java
redis 127.0.0.1:6379> EXISTS w3cschoolcc-new-key
(integer) 0
```

现在我们创建一个名为 w3cschoolcc-new-key 的键并赋值，再使用 EXISTS 命令。

```java
redis 127.0.0.1:6379> set w3cschoolcc-new-key newkey
OK
redis 127.0.0.1:6379> EXISTS w3cschoolcc-new-key
(integer) 1
redis 127.0.0.1:6379>
```

# Redis Expire 命令 - seconds 为给定 key 设置过期时间。

**Redis Expire 命令用于设置 key 的过期时间。key 过期后将不再可用。**

## 语法

redis Expire 命令基本语法如下：

```java
redis 127.0.0.1:6379> Expire KEY_NAME TIME_IN_SECONDS
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

设置成功返回 1 。 当 key 不存在或者不能为 key 设置过期时间时(比如在低于 2.1.3 版本的 Redis 中你尝试更新 key 的过期时间)返回 0 。

## 实例

首先创建一个 key 并赋值：

```java
redis 127.0.0.1:6379> SET w3ckey redis
OK
```

为 key 设置过期时间：

```java
redis 127.0.0.1:6379> EXPIRE w3ckey 60
(integer) 1
```

以上实例中我们为键 w3ckey 设置了过期时间为 1 分钟，1分钟后该键会自动删除。

# Redis Expireat 命令 - EXPIREAT 的作用和 EXPIRE 类似，都用于为 key 设置过期时间。 不同在于 EXPIREAT 命令接受的时间参数是 UNIX 时间戳(unix timestamp)。

**Redis Expireat 命令用于以 UNIX 时间戳(unix timestamp)格式设置 key 的过期时间。key 过期后将不再可用。**

## 语法

redis Expireat 命令基本语法如下：

```java
redis 127.0.0.1:6379> Expireat KEY_NAME TIME_IN_UNIX_TIMESTAMP
```

可用版本

```java
>= 1.0.0
```

**返回值**

设置成功返回 1 。 当 key 不存在或者不能为 key 设置过期时间时(比如在低于 2.1.3 版本的 Redis 中你尝试更新 key 的过期时间)返回 0 。

## 实例

首先创建一个 key 并赋值：

```java
redis 127.0.0.1:6379> SET w3ckey redis
OK
```

为 key 设置过期时间：

```java
redis 127.0.0.1:6379> EXPIREAT w3ckey 1293840000
(integer) 1
EXISTS w3ckey
(integer) 0
```

# Redis PEXPIREAT 命令 - 设置 key 的过期时间亿以毫秒计。

Redis PEXPIREAT 命令用于设置 key 的过期时间，已毫秒技。key 过期后将不再可用。

## 语法

redis PEXPIREAT 命令基本语法如下：

```java
redis 127.0.0.1:6379> PEXPIREAT KEY_NAME TIME_IN_MILLISECONDS_IN_UNIX_TIMESTAMP
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

设置成功返回 1 。 当 key 不存在或者不能为 key 设置过期时间时(比如在低于 2.1.3 版本的 Redis 中你尝试更新 key 的过期时间)返回 0 。

## 实例

首先创建一个 key 并赋值：

```java
redis 127.0.0.1:6379> SET w3ckey redis
OK
```

为 key 设置过期时间：

```java
redis 127.0.0.1:6379> PEXPIREAT tutorialspoint 1555555555005
(integer) 1
```

# Redis Keys 命令 - 查找所有符合给定模式( pattern)的 key 。

Redis Keys 命令用于查找所有符合给定模式 pattern 的 key 。。

## 语法

redis KEYS 命令基本语法如下：

```java
redis 127.0.0.1:6379> KEYS PATTERN
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

符合给定模式的 key 列表 (Array)。

## 实例

首先创建一些 key，并赋上对应值：

```java
redis 127.0.0.1:6379> SET w3c1 redis
OK
redis 127.0.0.1:6379> SET w3c2 mysql
OK
redis 127.0.0.1:6379> SET w3c3 mongodb
OK
```

查找以 w3c 为开头的 key：

```java
redis 127.0.0.1:6379> KEYS w3c*
1) "w3c3"
2) "w3c1"
3) "w3c2"
```

获取 redis 中所有的 key 可用使用 *。

```java
redis 127.0.0.1:6379> KEYS *
1) "w3c3"
2) "w3c1"
3) "w3c2"
```

# Redis Move 命令 - 将当前数据库的 key 移动到给定的数据库 db 当中。

Redis MOVE 命令用于将当前数据库的 key 移动到给定的数据库 db 当中。

## 语法

redis Move 命令基本语法如下：

```java
redis 127.0.0.1:6379> MOVE KEY_NAME DESTINATION_DATABASE
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

移动成功返回 1 ，失败则返回 0 。

## 实例

```java
# key 存在于当前数据库
 
redis> SELECT 0                             # redis默认使用数据库 0，为了清晰起见，这里再显式指定一次。
OK
 
redis> SET song "secret base - Zone"
OK
 
redis> MOVE song 1                          # 将 song 移动到数据库 1
(integer) 1
 
redis> EXISTS song                          # song 已经被移走
(integer) 0
 
redis> SELECT 1                             # 使用数据库 1
OK
 
redis:1> EXISTS song                        # 证实 song 被移到了数据库 1 (注意命令提示符变成了"redis:1"，表明正在使用数据库 1)
(integer) 1
 
 
# 当 key 不存在的时候
 
redis:1> EXISTS fake_key
(integer) 0
 
redis:1> MOVE fake_key 0                    # 试图从数据库 1 移动一个不存在的 key 到数据库 0，失败
(integer) 0
 
redis:1> select 0                           # 使用数据库0
OK
 
redis> EXISTS fake_key                      # 证实 fake_key 不存在
(integer) 0
 
 
# 当源数据库和目标数据库有相同的 key 时
 
redis> SELECT 0                             # 使用数据库0
OK
redis> SET favorite_fruit "banana"
OK
 
redis> SELECT 1                             # 使用数据库1
OK
redis:1> SET favorite_fruit "apple"
OK
 
redis:1> SELECT 0                           # 使用数据库0，并试图将 favorite_fruit 移动到数据库 1
OK
 
redis> MOVE favorite_fruit 1                # 因为两个数据库有相同的 key，MOVE 失败
(integer) 0
 
redis> GET favorite_fruit                   # 数据库 0 的 favorite_fruit 没变
"banana"
 
redis> SELECT 1
OK
 
redis:1> GET favorite_fruit                 # 数据库 1 的 favorite_fruit 也是
"apple"
```

# Redis PERSIST 命令 - 移除 key 的过期时间，key 将持久保持。

Redis PERSIST 命令用于移除给定 key 的过期时间，使得 key 永不过期。

## 语法

redis PERSIST 命令基本语法如下：

```java
redis 127.0.0.1:6379> PERSIST KEY_NAME
```

**可用版本**

```java
>= 2.2.0
```

**返回值**

当过期时间移除成功时，返回 1 。 如果 key 不存在或 key 没有设置过期时间，返回 0 。

## 实例

```java
redis> SET mykey "Hello"
OK
 
redis> EXPIRE mykey 10  # 为 key 设置生存时间
(integer) 1
 
redis> TTL mykey
(integer) 10
 
redis> PERSIST mykey    # 移除 key 的生存时间
(integer) 1
 
redis> TTL mykey
(integer) -1
```

# Redis Pttl 命令 - 以毫秒为单位返回 key 的剩余的过期时间。

Redis Pttl 命令以毫秒为单位返回 key 的剩余过期时间。

## 语法

redis Pttl 命令基本语法如下：

```java
redis 127.0.0.1:6379> PTTL KEY_NAME
```

可用版本

```java
>= 2.6.0
```

**返回值**

当 key 不存在时，返回 -2 。 当 key 存在但没有设置剩余生存时间时，返回 -1 。 否则，以毫秒为单位，返回 key 的剩余生存时间。

注意：在 Redis 2.8 以前，当 key 不存在，或者 key 没有设置剩余生存时间时，命令都返回 -1 。

## 实例

```java
# 不存在的 key
 
redis> FLUSHDB
OK
 
redis> PTTL key
(integer) -2
 
 
# key 存在，但没有设置剩余生存时间
 
redis> SET key value
OK
 
redis> PTTL key
(integer) -1
 
 
# 有剩余生存时间的 key
 
redis> PEXPIRE key 10086
(integer) 1
 
redis> PTTL key
(integer) 6179
```

# Redis TTL 命令 - 以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)。

Redis TTL 命令以秒为单位返回 key 的剩余过期时间。

## 语法

redis TTL 命令基本语法如下：

```java
redis 127.0.0.1:6379> TTL KEY_NAME
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

当 key 不存在时，返回 -2 。 当 key 存在但没有设置剩余生存时间时，返回 -1 。 否则，以毫秒为单位，返回 key 的剩余生存时间。

注意：在 Redis 2.8 以前，当 key 不存在，或者 key 没有设置剩余生存时间时，命令都返回 -1 。

## 实例

```java
# 不存在的 key
 
redis> FLUSHDB
OK
 
redis> TTL key
(integer) -2
 
 
# key 存在，但没有设置剩余生存时间
 
redis> SET key value
OK
 
redis> TTL key
(integer) -1
 
 
# 有剩余生存时间的 key
 
redis> EXPIRE key 10086
(integer) 1
 
redis> TTL key
(integer) 10084
```

# Redis RANDOMKEY 命令 - 从当前数据库中随机返回一个 key 。

Redis RANDOMKEY 命令从当前数据库中随机返回一个 key 。

## 语法

redis RANDOMKEY 命令基本语法如下：

```java
redis 127.0.0.1:6379> RANDOMKEY 
```

**可用版本**

```java
>= 1.0.0
```


**返回值**

当数据库不为空时，返回一个 key 。 当数据库为空时，返回 nil 。

## 实例

```java
# 数据库不为空
 
redis> MSET fruit "apple" drink "beer" food "cookies"   # 设置多个 key
OK
 
redis> RANDOMKEY
"fruit"
 
redis> RANDOMKEY
"food"
 
redis> KEYS *    # 查看数据库内所有key，证明 RANDOMKEY 并不删除 key
1) "food"
2) "drink"
3) "fruit"
 
 
# 数据库为空
 
redis> FLUSHDB  # 删除当前数据库所有 key
OK
 
redis> RANDOMKEY
(nil)
```

# Redis Rename 命令 - 修改 key 的名称

Redis Rename 命令用于修改 key 的名称 。

## 语法
redis Rename 命令基本语法如下：

```java
redis 127.0.0.1:6379> RENAME OLD_KEY_NAME NEW_KEY_NAME
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

改名成功时提示 OK ，失败时候返回一个错误。

当 OLD_KEY_NAME 和 NEW_KEY_NAME 相同，或者 OLD_KEY_NAME 不存在时，返回一个错误。 当 NEW_KEY_NAME 已经存在时， RENAME 命令将覆盖旧值。

## 实例

```java
# key 存在且 newkey 不存在
 
redis> SET message "hello world"
OK
 
redis> RENAME message greeting
OK
 
redis> EXISTS message               # message 不复存在
(integer) 0
 
redis> EXISTS greeting              # greeting 取而代之
(integer) 1
 
 
# 当 key 不存在时，返回错误
 
redis> RENAME fake_key never_exists
(error) ERR no such key
 
 
# newkey 已存在时， RENAME 会覆盖旧 newkey
 
redis> SET pc "lenovo"
OK
 
redis> SET personal_computer "dell"
OK
 
redis> RENAME pc personal_computer
OK
 
redis> GET pc
(nil)
 
redis:1> GET personal_computer      # 原来的值 dell 被覆盖了
"lenovo"
```

# Redis Renamenx 命令 - 仅当 newkey 不存在时，将 key 改名为 newkey 。

Redis Renamenx 命令用于在新的 key 不存在时修改 key 的名称 。

## 语法
redis Renamenx 命令基本语法如下：

```java
redis 127.0.0.1:6379> RENAMENX OLD_KEY_NAME NEW_KEY_NAME
```

**可用版本**

```java
>= 1.0.0
```

**返回值**

修改成功时，返回 1 。 如果 NEW_KEY_NAME 已经存在，返回 0 。

## 实例

```java
# newkey 不存在，改名成功
 
redis> SET player "MPlyaer"
OK
 
redis> EXISTS best_player
(integer) 0
 
redis> RENAMENX player best_player
(integer) 1
 
 
# newkey存在时，失败
 
redis> SET animal "bear"
OK
 
redis> SET favorite_animal "butterfly"
OK
 
redis> RENAMENX animal favorite_animal
(integer) 0
 
redis> get animal
"bear"
 
redis> get favorite_animal
"butterfly"
```

# Redis Type 命令 - 返回 key 所储存的值的类型。

Redis Type 命令用于返回 key 所储存的值的类型。

## 语法

redis Renamenx 命令基本语法如下：

```java
redis 127.0.0.1:6379> TYPE KEY_NAME 
```

**可用版本** 

```java
>= 1.0.0
```

**返回值**

返回 key 的数据类型，数据类型有：

none (key不存在)

string (字符串)

list (列表)

set (集合)

zset (有序集)

hash (哈希表)

## 实例

```java
# 字符串
 
redis> SET weather "sunny"
OK
 
redis> TYPE weather
string
 
 
# 列表
 
redis> LPUSH book_list "programming in scala"
(integer) 1
 
redis> TYPE book_list
list
 
 
# 集合
 
redis> SADD pat "dog"
(integer) 1
 
redis> TYPE pat
set
```