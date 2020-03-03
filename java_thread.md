## Thread的状态
###  线程有6种状态
* New：创建一个线程还没有start
* Runnable：就绪（ready）和运行（running）统称为运行。**线程对象**创建后调用start，线程对象位于可运行线程池中，等待线程调度选中获取cpu使用权， 此时为ready状态；线程对象获得cpu使用权为running
* Blocked：阻塞于锁
* Waiting：进入此状态的线程需要等待其他线程的动作
* Timed_waiting：在指定时间之后自行返回
* Terminated：线程执行完毕

### 线程函数与状态
* start()：将线程对象放入就绪队列中等待获取cpu，状态为ready
* sleep(time)：线程进入timed_waiting状态，time时间到了之后，转为ready状态，不释放锁
* wait()/waiti(long)：线程进入waiting，如果wait(long)进入timed_waiting状态，释放锁
* jion()/jion(long)：线程进入waiting，如果jion(long)进入timed_waiting，不释放锁
* yield()：线程进入ready，等待获取cpu，这个函数无法保证让步成功，因为调度选取为随机。有可能会马上获取到cpu，不释放锁
* notify()/notifyAll()/unpark()：线程进入ready，等待获取cpu；waiting/time_wating状态的线程可以通过此函数转换为ready状态

### 线程状态与锁
线程为ready是等待获取锁，获取到锁running，获取锁失败为blocked，循环试图获取锁成功running。

## 线程实现
## 锁
## park与unpark
