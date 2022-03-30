# Redis

## 底层
1. 使用IO多路复用
2. 非CPU密集型任务
3. 纯内存操作
4. 巧妙数据结构

> 底层是一个大Map，key是字符串，value可能是字符串，哈希，列表等。
> C语言实现，结构体redisObject

## 基础


## 命令

| 命令   | 说明              | 用法                          |
| ------ | ----------------- | ----------------------------- |
| SETNX  | set if not exists | setnx key [seconds] value     |
| PSETNX | set               | psetnx key milliseconds value |



### [keys](https://redis.io/commands/keys/)
1. keys命令是通过遍历全部db下的key再过滤实现的
2. keys命令没有汇总各节点查询结果的逻辑，不会路由keys命令
3. 设计目的是 调试或者特殊用途的，不适用于生产环境。
4. 可以使用``SCAN`` 或者 ``sets``


## 分布式锁

### 特性

1. 互斥性
2. 高可用性
3. 防止锁超时
4. 独占性

### 实现分布式锁有哪些坑
1. 不是原子操作
2. 没有释放锁
3. 释放了锁，但业务还没有执行完
4. 释放了别人的锁
5. 大量请求竞争锁失败
6. 多节点Redis主从复制问题
7. 高并发下锁的性能问题



## Websites

1. [Redis Launchpad](https://launchpad.redis.com/)
> Redis官方的用户展示厅，展示各种使用 Redis 的网络应用，并有用法和架构的讲解
2. 