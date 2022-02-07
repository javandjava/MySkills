- 基础

  - 变量类型注解: `var a:String` 
  - 元祖(tuples): (,),元祖给单个元素命名
  - 可选类型:`var a:String?`
  - 断言:assert(,)
  - 强制执行先决条件:precondiction(,)

- 运算符

  - 空合运算: ?? `a??b` a为nil返回b
  - 区间运算符: a...b,a..<b,[i...],[..<i]

- 集合类型

  - Array
    - 遍历：`for  t in array` ,`for (index,v) in array.enumerated()`
  - Sets
  - Dictionary:`var d:[Int:String]=[:]`,`var d:[Int,String]=[1:"one",2:"two"]`

- 字符串

  - 插值  `"\()"`
  - substring: 共享内存，当substring背修改时，会copysubstring，修改的这个copy
  - 前缀/后缀相等hasPrefix,hasSuffix

- 控制流

  - for in:`for inddex in 1...5 {}` ,`for t in stride(from: ,through: ,by:)` 
  - while,repeat-while
  - if
  - switch
    - 不存在隐式贯穿,可以匹配多个，但匹配到第一个就停止。
    - 贯穿需要使用 fallthrough
    - 区间匹配:case 1...<5
    - 元祖匹配:case (x,y), 匹配所有 `case (_,0)`第一个可以匹配到任何值，第二个匹配0
    - 值绑定:`case let (x,0)`如果匹配，x被赋值为第一个值
    - where:`case let (x,y) where x==y:`如果匹配x,y被匹配
    - 复合cases:`case 1,2,3,4,5:`
  - continue
  - break
  - label
  - guard:`guard  else`
  - 检测api可用:`available(iOS 10,macOS 10.12,*)`

- 函数

  - 定义:`func 函数名(参数标签 参数名:参数类型)->返回类型{}`
  - 多返回值:`->(r1:type,r2:type)`
  - 返回元祖可选:`->()?`
  - 隐式返回函数:`func fn(for p1:String)->String{ "return "+p1 }`
  - 参数标签和参数名称:参数名字之前添加参数标签，空格分割，_忽略标签
  - 默认参数:默认参数放在参数列表的最后
  - 可变参数:`(p:Int...)`
  - 输入输出参数:`func fn(l p:inout type){}` 调用 fn(&p),参数在函数中默认是不可改变的，定义为输入输出参数(inout)才可以改变这个参数
  - 函数类型:`(Int,Int)->Int`
  - 使用函数类型:`var a:(Int,Int)->Int,a(1,2)`
  - 函数类型作为函数参数：`func fn(_ f:(Int,Int)->Int)->{}`
  - 函数类型作为函数返回类型:`func fn()->(Int,Int)->Int{}`
  - 嵌套函数:`func fn()->{func f()->Int{}}`

- 闭包

  - 表达式:`{(p1:String,p2:String)-> Bool in return p1>p2}`,`({p1,p2 in return p1>p2}) `,`({p1,p2 in p1>p2})`,`({by:$0>$1})`,`(by:>)`
  - 尾随闭包:`(){}`
  - 值捕获:
    - 闭包为引用类型
  - 逃逸闭包:`@escaping`
  - 自动闭包:`@autoclosure`

- 枚举

  - `enum  {case , ,}`

  - 枚举成员遍历:`enum b:CaseIterable{}`遍历`for i in b.allCase {}`

  - 关联值:`enum barcode { case upc(Int,Int,Int,Int);case qrCode(String)}`,使用`var p=barcode.upc(1,2,3,4),p=.qrCode("")`

  - 原始值:`enum ascii:Character{ case tab="\t"}`,使用原始值初始化 `let a=ascii(rawValue:"\t")`

  - 递归:key indirect  可以在enum前，或者case前

     `indirect enum arithmetic {case number(Int) case add(arithmetic,arithmetic)}`

    `let five=arithmetic.number(5);let four=arithmetic.number(4);let sum=arithmetic.number.add(five,four)`
  
- 类和结构体
  
  - 定义语法:`struct SomeStruct{}`,`class SomeClass{}`
  - 结构体的成员逐一构造器
  - 结构体，枚举为值类型
  - 类是引用类型：需要恒等===判断是否为一个实例
  - 属性
    - 存储属性:不能用于枚举，延时加载`lazy`
    - 计算属性:用于类，结构体，枚举。就是一个获取数值的函数组合`var p:type { get { return type} set{}}`
      - 简化setter：set函数入参 的参数名称默认为newValue
      - 简化getter:get函数可以去掉return
    - 只读计算属性:只有getter，没有setter
    - 属性观察器:可用在自定义的存储属性，继承的存储属性，继承的计算属性
      - willset:新值设置之前，默认参数名newValue
      - didset:新值设置之后，默认参数名oldValue
    - 属性包装器:`@properWrapper`定义一个属性包装器，再将这个属性包装器写在属性定义之前`@properWrapper struct min{ private var num=0 var wrapperValue:{}};stuct t{ @min var h:Int}`
    - 设置属性的初始值:`init(p:Int){}`使用`@min(p:1) var h:Int`
    - 从属性包装器呈现一个值：`$`
    - 全局变量和局部变量:
    - 类型属性(类的静态变量):`static var p:type`
  - 方法
    - 定义范围:类，结构体，枚举
    - self
    - 可变方法：`mutating func(){}`,应为结构体和枚举为值类型，在方法中是无法改变属性的，为了能改变属性需要将方法变成可变行为
    - 类型方法:`static func f(){}`
  - 下标:`subscript()->Type {get{} set{}}`
  - 继承
    - 语法:`class subClass:fatherClass{}`
    - 重写:`override func fn(){}`
    - 防止重写:`final`
  - 构造过程
    - 初始赋值:默认值和构造器，不会触发属性观察者
    - 构造器:`init(){}`,常量属性可以在构造器中赋值，之后再不可以修改
    - 形参构造过程:`init(label name:Type){}`
    - 可选属性:`var p:Type?`
    - 结构体会有一个默认构造器(逐一构造器)
    - 指定构造器:必须调用父类的指定构造器
    - 遍历构造器:`convenience init(){}`,必须调用其他构造器，最后必须调用指定构造器
    - 两段式构造:
      1. 存储属性赋值默认值
      2. 新实例准备使用之前进一步定义他们的存储属性
    - 构造器的继承
      - 默认情况下子类不继承父类构造器
      - 继承父类构造器：子类没有指定构造器，子类提供了所有父类指定构造器的实现
    - 可失败构造器:`init?(){}`,`init!(){}`
    - 必要构造器:`required init() {}`
    - 析构函数:`deinit(){}` 只能使用在类中
    - 可选链:
    - 访问可选类型的下标
  
- 错误处理
  
  - 抛出错误:`throw`
  - 处理错误
  - 传递错误:throwing,`func fn() throws->String `
  - 处理错误:`do{} catch p {} catch {}`
  - 将错误转换成可选值:`try?fun` 没错误，获取函数返回值，否则喂nil
  - 禁用错误传递:`try!fun`
  - 指定清理操作:`defer {}`，defer{}中的代码会延迟执行，在当前作用域之前执行。
  
- 并发
  
  - 定义:`func fn() async -> Type {}`
  - 调用：`await func()`
  - 异步序列:`for try await    in    `
  - 并行调用:`await let `
  - 任务和任务组:
  - Task
  - Actors
  
- 类型转换
  
  - 类型检查:`is`
  - 向下转型:`as?,as!`，?向下转型失败返回nil，!失败会触发运行时错误
  - Any 任何类型，函数类型；AnyObject 任何类类型

- 嵌套类型
  
- 扩展
  
  - 语法:`extension class: `
  - 可扩展:计算属性，构造器，方法，可变实例方法，下标，嵌套类型
  
- 协议

  - 定义:`protocol{}`
  - 遵循协议：` : 协议名`;多个协议之间使用,；先类后协议
  - 属性的可读可写:`var p {get set}`
  - 异变方法(改变实例属性):`mutating`
  - 构造器要求:协议要求构造器，实现时需要加上`required`
  - 协议作为类型
  - 范型有条件的遵循协议:`where`
  - 先实现协议后声明遵循:类型已经实现协议中的所要求，可以`extension 协议 {}`方式后声明遵循
  - 协议继承
  - 类专属协议:`:AnyObject`
  - 协议组合: `func (p1&p2){}`参数需要遵循p1和p2协议
  - 可选协议要求：协议的要求可选 `@objc protocolp{ @objc option var v @objc option func(){}}`
  - 协议扩展:提供默认实现；添加限制条件

- 范型

  - 范型函数:`func fn<T>(_ a:inout T)` T为类型参数
  - 范型类型:`struct s<T>{}`
  - 范型扩展:原始类型定义中声明的类型参数列表可以在扩展中直接使用
  - 类型约束:`struct s <T:class,U:protocol>{}`T必须是class的子类，U必须符合protocol协议
  - 关联类型:`associatedtype` 实现`typealias`
  - 范型where
  - 包含上下文关系的where分句

- 不透明类型

  - 返回不透明类型:`func fun()->some T{}`

- 自动引用计数器

  - 解决实例间循环引用的2个方法：1，弱引用；2，无主引用
  - 弱引用:`weak`
  - 无主引用:`unowned`
  - 闭包解决循环强引用:定义捕获列表:`[unowned self,weak d]()->Type{}`

- 内存安全

- 访问控制

  - open和public:
  - internal:同一模块，源文件访问
  - fileprivate:只能文件内部访问
  - private:定义的作用域内部，和extension
  - 默认访问级别:internal

- 高级运算符

  - 位运算:~,&,|,^,<<,>>
  - 运算符重载
  - 前缀和后缀运算符（一元运算符重载）:`static prefic func - ()->Type {}`
  - 自定义运算符:
    1. 全局定义:`prefix operator +++`
    2. 实现:`extension S { static prefix func +++ ()->Type {}}`
  - 自定义运算符优先级
    1. `infix operator +-:AdditionPrecddence`
    2. `extension S{static func +-()->Type{}}`
    3. +-属于AdditionPrecddence优先组
  - 结果构造器：`@resultBuilder`

  

  

  