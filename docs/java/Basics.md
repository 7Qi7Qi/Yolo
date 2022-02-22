# 基础



## 内部类

#### 一、成员内部类，也称作普通内部类

```java
//外部类Outer
public class Outer {
    private int a = 99; //外部类私有属性
    public class Inner {
        int b = 2 ;
        public void test() {
            System.out.println("访问外部类中的a：" + a);
            System.out.println("访问内部类中的b：" + );
        }
    }
    //测试成员内部类
    public static void main (String[] args) {
        Outer o = new  Outer(); //创建外部类对象
        Inner i = o.new Inner(); //使用外部类对象创建内部类对象
        i.test(); //调用内部类对象的test方法
    }
}
```

> 1. 内部类相当于外部类成员变量的位置，可以使用任意访问修饰符，public、private、protected、default
> 2. 

