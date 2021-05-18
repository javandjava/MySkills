

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

# jdk8 新特性
## 时间戳与string转换 
```
DateTimeFormatter formatter=DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
//转string
LocalDateTime parse = LocalDateTime.parse(str, formatter);
LocalDateTime.from(parse).atZone(ZoneId.systemDefault()).toInstant().toEpochMilli();

//转long
formatter.format(LocalDateTime.ofInstant(Instant.ofEpochMilli(timestamp),ZoneId.systemDefault()))

```

## Predicate
1. jdk8提供的函数接口，提供抽象方法的test，返回true/false，有默认的and,or,negate,isEqual
```
Simaple
Predicate<String> predicate = item -> "测试".equals(item);
predicate.test("hello")

and
Predicate<Integer> p1 = t -> t > 3;
p1=p1.and(t->t<6)
返回 >3 and <6的数字

```

## Function
1. 函数式接口,只有一个抽象方法`apply，R apply(T t)`,2个默认方法`compose`,`andThen`
```
Sample
Function<Integer, Integer> function1 = value -> value * 2;
Function<Integer, Integer> function2 = value -> value + 3;
Function<Integer, Integer> function3 = function1.compose(function2);
Function<Integer, Integer> function4 = function1.andThen(function2);

function3.apply(2) 结果为(2+3)*2=10
function4.apply(2) 结果为2*2+3=7

```

## BiFunction
1. Function的一个扩展，接受2个参数，返回一个参数`R apply(T t, U u)`,`<V> BiFunction<T, U, V> andThen(Function<? super R, ? extends V> after)`
```
BiFunction<Integer, Integer, Integer> biFunction = (num1, num2) -> num1 + num2;
// 输出 : 5
System.out.println(biFunction.apply(2, 3));
Function<Integer,Integer> function = num -> num * num;
// newBiFunction的apply(num1, num2)方法等于function.apply(biFunction(num1, num2))
BiFunction<Integer, Integer, Integer> newBiFunction = biFunction.andThen(function);
// 输出 : 25
System.out.println(newBiFunction.apply(2, 3));
```


