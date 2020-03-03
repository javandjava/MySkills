## HashMap
1. 底层实现：数组+链表/红黑树(链表超过8个，转为红黑树)

##  Lambda
* Lambda本质为匿名函数
*  组成 ：参数列表，->，函数体，函数体可以是表达式也可以是语句块   

```
List<Player> players
for (Player p:players){
	System.out.print(p)
}

players.forEach(p->System.out.println(p))
players.forEach(System.out::println)

```

## ArrayList 扩容
1. ArrayList初始化默认容量为10
2. 当容量不够时，按照当前容量的1.5倍扩容