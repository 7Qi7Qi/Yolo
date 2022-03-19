# Q & A

1. 集合并行流中的Spring事务会生效吗？
   1. parallelStream()：ForkJoinPool.commonPool.worker
   2. 一般来说并行流会新建线程去执行方法，而Spring的事务只会保证主线程的事务会回滚，其他线程事务不会回滚
   3. ThreadLocal实现的事务（保存的数据库连接）。 [详见](../framework/Spring.md#事务)
   4. 所以不要再并行流中使用ThreadLocal、数据库事务