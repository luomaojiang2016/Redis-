# Redis-
缓存是分布式系统的重要组成部分，主要解决高并发大数据环境下热点数据访问的性能问题，提供高性能的数据访问
#Redis基本数据类型
1:string 
string是redis最基本的类型，一个key对应一个value。
string类型是二进制安全的。意思是redis的string可以包含任何数据。比如jpg图片或者序列化的对象 。
string类型是Redis最基本的数据类型，一个键最大能存储512MB。
可用于存储热点数据，验证码等。
2：List
List类型是按照插入顺序排序的字符串链表。和数据结构中的普通链表一样，我们可以在其头部(left)和尾部(right)添加新的元素。在插入时，如果该键并不存在，Redis将为该键创建一个新的链表。与此相反，如果链表中所有的元素均被移除，那么该键也将会被从数据库中删除。
List中可以包含的最大元素数量是4294967295。可用于消息队列，top 热点 数据等
3:Set
Set 也存储了列表集合，并可以去重，并提供了交集，差集
4:hash
 redis hash是一个键值对集合（k=>value）,它特别适合存储对象

#Redis常见问题及解决方案
缓存穿透:
   缓存穿透是指查询一个一定不存在的数据，由于缓存是不命中时被动写的，并且出于容错考虑，如果从存储层查不到数据则不写入缓存，这将导致这个不存在的数据每次请求都要到存储层去查询，失去了缓存的意义。在流量大时，可能DB就挂掉了，要是有人利用不存在的key频繁攻击我们的应用，这就是漏洞。 
解决方案：可以使用布隆过滤器，或者把访问不存在的结果也存到缓存
缓存雪崩：
缓存雪崩是指缓存中数据大批量到过期时间，而查询数据量巨大，引起数据库压力过大甚至down机。和缓存击穿不同的是,缓存击穿指并发查同一条数据，缓存雪崩是不同数据都过期了，很多数据都查不到从而查数据库。
解决方案：
缓存数据的过期时间设置随机，防止同一时间大量数据过期现象发生。
如果缓存数据库是分布式部署，将热点数据均匀分布在不同搞得缓存数据库中。
设置热点数据永远不过期。
缓存击穿
 缓存击穿是指缓存中没有但数据库中有的数据（一般是缓存时间到期），这时由于并发用户特别多，同时读缓存没读到数据，又同时去数据库去取数据，引起数据库压力瞬间增大，造成过大压力
解决方案
设置热点数据永远不过期。
加互斥锁







