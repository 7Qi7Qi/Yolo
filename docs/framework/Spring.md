# Spring

## SpringBoot

### 注解

#### Autowired

##### required属性
+ **@Autowired(required = true)**
  + 默认是true，表示注入的时候，该bean必须存在，否则会注入失败

+ **@Autowired(required = false)**
  + 忽略当前要注入bean，如果有直接注入，没有跳过，不会报错

+ 容器启动过程中，会初始化bean，spring核心之一（IOC）
+ ~~当前容器不能注入自己，这样就会不停的注入自己，陷入死循环，从而找不到要注入的bean~~
  + Spring框架提供的三级缓存来专门解决循环依赖
  + 构造函数注入会进入死循环



## SpringCloud

