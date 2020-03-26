### 自旋锁
为了不放弃CPU执行事件，循环使用CAS技术对数据尝试进行更新，直到成功
```java
package org.by.heart.study;

import java.lang.reflect.Field;

import sun.misc.Unsafe;

/**
 * 利用底层内存的CAS原理实现原子性操作
 * 
 * @author 彭嘉辉
 *
 */
public class LockDemo1 {
	volatile int value = 0;

	static Unsafe unsafe;

	private static long valueOffset;

	static {
		try {
			// 通过反射拿到Unsafe对象
			Field field = Unsafe.class.getDeclaredField("theUnsafe");
			field.setAccessible(true);
			unsafe = (Unsafe) field.get(null);

			// 得到value属性在内存中的偏移量
			valueOffset = unsafe.objectFieldOffset(LockDemo1.class.getDeclaredField("value"));
		} catch (Exception e) {
			e.printStackTrace();
		}

	}

	public void add() {
		int current;
		//--------自旋锁--------//
		do {
			// CAS的原子性操作，如果操作很耗时，线程会等这个循环，占用大量CPU运行时间
			// 每次拿到最新的内存值
			current = unsafe.getIntVolatile(this, valueOffset);
		} while (!unsafe.compareAndSwapInt(this, valueOffset, current, current + 1));// 加1失败了就重试
		//--------自旋锁--------//
	}

	public static void main(String[] args) throws InterruptedException {
		LockDemo1 demo = new LockDemo1();
		for (int i = 0; i < 2; i++) {
			new Thread(() -> {
				for (int j = 0; j < 10000; j++) {
					demo.add();
				}
			}).start();
		}
		Thread.sleep(2000L);
		System.out.println(demo.value);
	}
}

```

### 悲观锁
假定会发生并发冲突，同步所有数据的相关操作，从读数据就开始上锁

### 乐观锁（自旋锁的另外一种说法）
假定没有冲突，修改数据时如果发现数据与之前所取得值不一致，读取最新的值，修改之后再执行更新操作

### 独享锁（读写锁）
给资源加上锁，线程可以修改资源，其他线程不能再加锁（单写）

### 共享锁（写锁）
给资源加上锁后只能读不能改，其他线程也只能给资源加读锁，不能加写锁（多读）