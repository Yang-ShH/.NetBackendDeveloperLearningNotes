# redis 支持的数据类型

redis 数据库支持五种数据类型：

- 字符串（string）

- 哈希（hash）

- 列表（list）

- 集合（set）

- 有序集合（sorted set）

- 位图（Bitmaps）

- 基数统计（HyperLogLogs）

  

## 字符串

string 是一组字节。在 redis 数据库中，字符串时二进制安全的。这意味着它们具有已知长度，并且不受任何特殊终止字符的影响。可以在一个字符串中存储最多512兆字节的内容。

~~~bash
SET name "young"
OK

GET name
"young"
~~~



## 哈希

哈希是键值对的集合。在 redis 中，哈希是字符串字段和字符串值之间的映射。因此，它们适合表示对象。

~~~bash
HMSET user1 username young password 123456
OK

HGETALL user1
"username"
"young"
"password"
"123456"
~~~

这里 user1 是key ，username是field，young是value



## 列表

redis 列表定义为字符串列表，按插入顺序排序。可以将元素添加到redis列表的头部或尾部。

~~~bash
lpush l1 1
(integer) 1

lpush l1 2
(integer) 1

lpush l1 3
(integer) 1

lpush l1 4
(integer) 1

rpush l1 0

lrange l1 0 10
1) "4"
2) "3"
3) "2"
4) "1"
5) "0"
~~~



## 集合

集合（set）是 redis 数据库中的无序字符串集合。在 redis 中，添加，删除和查找的时间复杂度是 O(1)。

~~~bash
sadd s1 1
(integer) 1

sadd s1 2
(integer) 1

sadd s1 2
(integer) 0

sadd s1 3
(integer) 1

sadd s1 4
(integer) 1

smembers s1
1) "1"
2) "2"
3) "3"
4) "4"
~~~

在上面的示例中，可以看到 2 被添加了多次，但由于该集的唯一属性，它只添加一次。



## 有序集合

redis 有序集合类似于 redis 集合，也是一组非重复的字符串集合。但是，排序集的每个成员都与一个分数相关联，该分数用于获取从最小到最高分数的有序排序集。虽然成员是独特的，但可以重复分数。

~~~
zadd [key] [score] [value]
ZRANGEBYSCORE 0 10
~~~

