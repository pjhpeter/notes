## 锁的类型
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
```java
// 悲观锁、独享锁
public class ObjectSyncDemo1 {
	
	// 不加static关键字的话是对象锁，每个类有自己的锁，不能实现同步效果
	// 加static关键字是类锁，所有对象抢同一把锁，可以实现同步
	// ---------悲观锁--------------//
	public synchronized static void test1() {
		try {
			System.out.println(Thread.currentThread() + "我开始执行了");
			Thread.sleep(3000L);
			System.out.println(Thread.currentThread() + "我结束执行了");
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
	// ---------悲观锁--------------//
	
	public static void main(String[] args) throws Exception{
		new Thread(() -> {
//			new ObjectSyncDemo1().test1();
			ObjectSyncDemo1.test1();
		}).start();
		
		Thread.sleep(1000L);
		
		new Thread(() -> {
//			new ObjectSyncDemo1().test1();
			ObjectSyncDemo1.test1();
		}).start();
	}
}
```


### 乐观锁（自旋锁的另外一种说法）
假定没有冲突，修改数据时如果发现数据与之前所取得值不一致，读取最新的值，修改之后再执行更新操作

### 独享锁（写锁）
给资源加上锁，线程可以修改资源，其他线程不能再加锁（单写）
> 悲观锁的代码效果也是独享锁的效果

### 共享锁（读锁）
给资源加上锁后只能读不能改，其他线程也只能给资源加读锁，不能加写锁（多读）

```java
public class ReentrantReadWriteLockDemo2 {

    private ReentrantReadWriteLock readWriteLock = new ReentrantReadWriteLock();

    public static void main(String[] args) {
        ReentrantReadWriteLockDemo2 readWriteLockDemo1 = new ReentrantReadWriteLockDemo2();

        new Thread(() -> {
            readWriteLockDemo1.read(Thread.currentThread());
        }).start();

        new Thread(() -> {
            readWriteLockDemo1.read(Thread.currentThread());
        }).start();

        new Thread(() -> {
            readWriteLockDemo1.write(Thread.currentThread());
        }).start();
    }

    // 使用读锁，读操作可以并发执行
    public void read(Thread thread) {
        readWriteLock.readLock().lock();
        try {
            long start = System.currentTimeMillis();
            while (System.currentTimeMillis() - start <= 1) {
                System.out.println(thread.getName() + "正在进行读操作");
            }
            System.out.println("读操作完毕");
        } finally {
            readWriteLock.readLock().unlock();
        }
    }

    // 使用写锁，只有一个线程可以写，且读锁没有释放，不能上写锁
    public void write(Thread thread) {
        readWriteLock.writeLock().lock();
        try {
            long start = System.currentTimeMillis();
            while (System.currentTimeMillis() - start <= 1) {
                System.out.println(thread.getName() + "正在进行写操作");
            }
            System.out.println("写操作完毕");
        } finally {
            readWriteLock.writeLock().unlock();
        }
    }

}
```

### 可重入锁、不可重入锁
线程拿到一把锁后，可以重复进入同一把锁所同步的其他代码
```java
// 可重入锁
public class ObjectSyncDemo2 {

	// ---------可重入锁--------------//
	public synchronized void test2(Object arg) {
		System.out.println(Thread.currentThread() + "我开始执行了" + arg);
		if (arg == null) {
			// 递归调用，同一个线程再次进入被锁方法，可以执行成功
			test2(new Object());
		}
		System.out.println(Thread.currentThread() + "我结束执行了" + arg);
	}
	// ---------可重入锁--------------//

	public static void main(String[] args) throws Exception {
		new ObjectSyncDemo2().test2(null);
	}
}
```

### 公平锁、非公平锁
争抢锁的顺序，如果是按先来后到的顺序则为公平锁

## 锁的升级
1. 偏向锁
JVM参数默认设置是可偏向的，也可以禁用，可偏向的情况下，synchornized关键字针对的对象，对象头的mark work会存一个线程id，说明这个锁偏向于这个线程，线程可以对对象加锁或者释放锁

2. 轻量级锁
在偏向锁的情况下，有其他线程想获取这把锁，但是发现mark work已经标记的其他线程的id，而且标记线程并未释放锁，此时其他线程会通过CAS循环尝试获得锁，这时锁会升级成轻量级锁

3. 重量级锁
在轻量锁的情况下，其他线程通过CAS循环获得锁的次数超过的一定数量（这个数量可以通过运行参数配置），锁会升级成重量级锁，停止其他线程CAS循环，进入阻塞

> 锁的升级实际上是JVM为了提升性能，减少计算机性能消耗的优化策略