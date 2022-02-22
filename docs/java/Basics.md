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
> 2. 内部类的方法可以访问外部类的变量，不受访问控制符限制
> 2. 实例化对象：new Outer().new Inner().test()
> 2. 相同变量名，内部类的可以直接访问，访问外部类的需要使用this关键字

#### 二、静态内部类

```java
public class HelloWorld{
    String name = "xx";
    public static class Inner {
        public void show() {
            System.out.println("访问外部类中的name：" + new HelloWorl().name);
        }
    }
}
```

> 1. 静态内部类不能直接访问外部类的非静态成员，需要实例化外部类再访问
> 2. 创建对象时，不需要使用外部来对象，可以直接创建
> 3. 相同变量名：外部类的需要使用 "类名.静态成员"

#### 三、方法内部类

```java
public class MOuter {
    public void show() {
        final int a = 25;
        int b = 13;
        class MInner {
            int c = 2;
            public void print() {
                System.out.println("访问外部类方法中的常量a：" + a);
                System.out.println("访问内部类的变量c：" + c);
            }
        }
        MInner mi = new MInner();
        mi.print();
    }
    
    public static void main(String[] args ) {
        MOuter mo = new Mouter();
        mo.show();
    } 
}
```

> 方法内部类无法在外部类的方法外的地方使用，因此方法内部类不能使用访问控制符和static 修饰符

