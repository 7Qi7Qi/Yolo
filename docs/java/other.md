# 其他

## 各种Object

> DO、DTO、BO、AO、VO、POJO 
>
> - DO （ Data Object ）：与数据库表结构一一对应，通过 DAO 层向上传输数据源对象。
> - DTO （ Data Transfer Object ）：数据传输对象，Service 或 Manager 向外传输的对象。
> - BO （ Business Object ）：业务对象。 由 Service 层输出的封装业务逻辑的对象。
> - AO （ Application Object ）：应用对象。 在 Web 层与 Service 层之间抽象的复用对象模型，极为贴近展示层，复用度不高。
> - VO （ View Object ）：显示层对象，通常是 Web 向模板渲染引擎层传输的对象。
> - POJO （ Plain Ordinary Java Object ）：在本手册中，POJO 专指只有 setter/getter/toString 的简单类，包括 DO/DTO/BO/VO 等。
>
> ![image-20220216221201297](../_assets/image-20220216221201297.png)

## Spring 依赖注入

### 三种依赖注入方式

#### Field Injection

> **@Autowired**
>
> 通过Java反射机制实现，所以private成员也可以被注入具体的对象
>
> ```java
> @Controller
> public class UserCotroller {
>     @Autowired
>     private UserService userService;
> }
> ```

#### Construction Injection （推荐）

> 通过对象构造的时候建立关系，所以对对象创建的顺序有要求。当然Spring会为你搞定这样的先后顺序，除非出现循环依赖，然后就会抛出异常
>
> ```java
> @Controller
> public class UserController {
>     private final UserService userService;
>     public UserController(UserService userService) {
>         this.userService = userService;
>     }
> }
> ```

#### Setter Injection

> 1. 也会用到**@Autowired** 注解，
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

#### 对比

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
