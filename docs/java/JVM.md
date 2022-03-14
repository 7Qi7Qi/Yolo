# JVM


## Tools

>  **jdk/bin目录下**。[参考链接](https://blog.csdn.net/youyou1543724847/article/details/84647552)


1. jar： jar包工具
2. javac：java程序编译器
3. javah：C头文件和stub文件生成器
4. javap：java反编译器
5. 监控工具
   1. jmap（java memory map）
   2. jvisualvm（gui监控工具）
   3. jconsole（gui监控工具）
      1. java mbean对象
   4. jstat
      1. jvm statistics monitoring tool
      2. jvm内建指令对应用资源和性能进行实时的命令行监控
   5. jmc（java mission control）
      1. jmx
      2.  java flight profile
   6. jhat
      1. java heap dump文件浏览器
6. jdb：java调试工具
7. 安全相关
   1. policy tool：gui策略工具
   2. keytool：密钥工具
   3. kinit、klist、ktab：kerberos管理工具
   4. jarsigner：签名、签名校验工具
8. rmiregistry

## OOM

> VM Option: -Xmx30m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/Java/logs
> 