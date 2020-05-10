## 预防参数
### 堆内存设置
-Xms：堆内存最小值

-Xms128m

-Xmx：堆内存最大值

-Xmx512m

> 最大堆内存设置不能占用太多系统资源，比如8g的服务器，设置成4g，这样即使内存溢出了，也不影响系统运行，保证顺利执行错误定位的命令：jmap、jstat、jstack等

### GC参数
-XX:+UseConcMarkSweepGC（选择垃圾回收器）

> 前台应用GC机制可使用UseConcMarkSweepGC（CMS+PartNew），并行回收，后台应用使用默认即可，GC机制会根据JDK版本不停更新，不是一尘不变
>
> 90%的情况下只需要调整垃圾回收器即可

## 问题定位
### FullGC造成系统停顿时间过长
当程序出现频繁FullGC时，表示程序可能即将出问题
```java
/**
 * 频繁使用System.gc导致FullGC次数过多
 * 
 * server模式运行，打印GC日志
 * 
 * -Xmx512m -server -verbose:gc -XX:+PrintGCDetails -Xloggc:filepath -XX:+HeapDumpOnOutOfMemoryError
 */
public class FullGCDemo1 {
    
    public static void main(String[] args) throws InterruptedException {
        for (int i = 0; i < 1000; i++) {
            byte[] b = new byte[1024 * 1024 * 256]; //256m
            System.gc();
            System.out.println("我GC了一次");
            Thread.sleep(2000L);
        }
    }
}
```

### 问题定位命令
jmap、jstat、jstack

```cmd
//查看进程id
> jcmd

//查看gc情况
> jstat -gc <进程id>
```
