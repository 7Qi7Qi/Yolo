# Redis

## 基础


## 命令

| 命令   | 说明              | 用法                          |
| ------ | ----------------- | ----------------------------- |
| SETNX  | set if not exists | setnx key [seconds] value     |
| PSETNX | set               | psetnx key milliseconds value |




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