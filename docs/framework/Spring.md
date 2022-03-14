# Spring

## SpringBoot

### Bean

作用域：Prototype/Singleton/Request/Session/Global Session

- Prototype：原型模式，每次获取bean都会创建以一个新的实例，因此不存在线程安全的问题。
- Singleton：不同的线程访问同一个bean，如果这个bean中含有实例变量，并且线程具有对实例变量的写操作时，就会产生线程安全问题
  - 解决：使用[ThreadLocal](../java/Concurrence.md#ThreadLocal)，为每个线程创建独立的变量副本，互相隔离互不影响

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

##### 依赖注入方式

###### 一、Field Injection

> **@Autowired**
>
> 通过Java反射机制实现，所以private成员也可以被注入具体的对象
>
> ```java
> @Controller
> public class UserCotroller {
>  @Autowired
>  private UserService userService;
> }
> ```

###### 二、Construction Injection （推荐）

> 通过对象构造的时候建立关系，所以对对象创建的顺序有要求。当然Spring会为你搞定这样的先后顺序，除非出现循环依赖，然后就会抛出异常
>
> ```java
> @Controller
> public class UserController {
>  private final UserService userService;
>  public UserController(UserService userService) {
>      this.userService = userService;
>  }
> }
> ```

###### 三、Setter Injection

> 1. 也会用到@Autowired注解，
> 2. 但使用方式与**Filed Injection**有所不同，Field Injection是用在成员变量上的，而Setter Injection是用在Setter函数上的。
> 3. 就是通过调用成员变量的set方法来注入想要使用的依赖对象
> 4. 相较于 **Field Injection** 测试性更好
>
> ```java
> @Controller
> public class UserController {
>     private UserService userService;
> 
>     @Autowired
>     public void setUserService(UserService userService) {
>         this.userService = userService;
>     }
> }
> ```
>
> 

###### 对比

| 注入方式              | 可靠性 | 可维护性 | 可测试性 | 灵活性 | 循环关系检测 | 性能影响 |
| --------------------- | :----: | :------: | :------: | :----: | :----------: | :------: |
| Field Injection       | 不可靠 |    差    |    差    |  灵活  |    不检测    |  启动快  |
| Constructor Injection |  可靠  |    好    |    好    | 不灵活 |   自动检测   |  启动慢  |
| Setter Injection      | 不可靠 |    差    |    好    |  灵活  |    不检测    |  启动快  |

> 1. 可靠性
>    1. 对象构建和使用过程，看对象在各阶段的使用是否可靠
>    2. 构造函数有严格的构建顺序和不可变性，一旦构建就可用，且不会被更改
> 2. 可维护性
>    1. 更容易阅读，分析依赖关系
>    2. 构造函数中可以明显分析出依赖关系
> 3. 可测试性
>    1. 在复杂的依赖关系下，更容易的编写单元测试来评判
>    2. Constructor Injection和 Setter Injection的方式更容易Mock和注入对象，更容易实现单元测试
> 4. 灵活性
>    1. 开发实现时候的编码灵活
>    2. Constructor Injection对Bean依赖关系有着严格的顺序要求
> 5. 性能影响
>    1. Constructor Injection 严格的顺序要求，会拉长启动时间

#### Resource

> javax.annotation.Resource

##### 和Autowire区别

> - Autowire
>   - 默认通过类型注入，如果存在多个类型则通过名称注入
>   - 可以使用@Primary定义类名，优先使用
>   - 使用@Qualifier("xxx")，指定类名注入 （合格者）
> - Resource
>   - 默认使用名称注入，如果名称找不到，则通过类型注入
> - bean默认是开头字母小写的类名

#### Transactional

+ 回滚rollbackFor()。默认是RuntimeException
  + IOException不是RuntimeException子类，不会进行事务回滚
```java
@Transactional(rollbackFor = IOException.class)
public class Clazz {
    
}
```


## SpringCloud

