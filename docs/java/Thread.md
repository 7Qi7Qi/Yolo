# 线程


## 线程池

### 拒绝策略
+ RejectedExecutionHandler，任务处理不过来时，拒绝策略

```java
import java.util.concurrent.ThreadPoolExecutor;

public interface RejectedExecutionHandler {
    void rejectedExecution(Runnable r, ThreadPoolExecutor executor);
}
```

1. new ThreadPoolExecutor.AbortPolicy()
   1. 直接抛异常
2. new ThreadPoolExecutor.CallerRunsPolicy()
   1. 线程池如果未关闭，直接执行run方法
3. new ThreadPoolExecutor.DiscardPolicy()
   1. 新任务直接丢弃
4. new ThreadPoolExecutor.DiscardOldestPolicy()
   1. 线程池等待任务移除队列头部元素（poll()方法），将新任务加到队列中
5. 自定义策略，比如持久化多余的线程，用定时任务把持久化线程取出