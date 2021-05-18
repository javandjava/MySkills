### 概念 
#### 虚拟DOM
### 项目
#### 安装react
1. react
2. react-dom
#### 搭建（webpack4.x）
1. npm init -y 初始化 
2. 建立目录结构 src，dist
3. src建立index.html, index.js
4. 安装webpack npm install webpack -g ;npm install webpack-cli -g /一定要全局安装
5. 建立webpack.config.js 
```
module.export={
    mode: 'development'
}
```
6. 开发时实时打包 安装 `webpack-dev-server`，配置`webpack-dev-server`

   ```json
   "dev": 'webpack-dev-server --host 127.0.0.1 --port 3000 '
   ```

   + 修改index.html 的`script` 为 `<script src=/main.js></script>` 打包的默认文件

7.  安装react，react-dom `npm install ract react-dom -S`

8. 开始创建react

   + 导入React，ReactDOM
   + 创建虚拟dom
   + 渲染到页面
   
9. 增加 省略后缀 `webpack.config.js`

```
resolve: {
        extensions:['js','jsx','json']
    },
```



#### js 中使用html

1. 使用`babel`处理html标签 `jsx`语法
2. 安装babel `babel-core`,`babel-loader`,`babel-plugin-transform`,`babel-preset-env`,`babel-preset-stage-0`,`babel-preset-react`
3. 增加babel配置 根目录下增加`.babelrc`文件：

```
{
 "presets":["env","stage-0","react"]
 "plugins":["transform-runtime"]
}
```



1. 增加webpack.config.js 的配置

```
module:{
 rules:[
 	{test:/\.js|jsx$/,use:'babel-loader',exclude: /'node_modules'/}
 ]
}
```



#### 创建组件

1. 方式一**`function`**

   ```jsx
   fucntion Com1(props){
   	return <div>{props.name}</div>
   }
   
   const v={"name":"v"}
   
   ReactDOM.render(<div>
       <Com1 name="v2"></Com1>
   </div>,document.getElementById('app'))
   
   ```

   + 无状态

2. 方式二**`class`**

```jsx
class c entends React.Component{
	constructor(){
		super()
		this.state={} //私有数据
	}
	render(){
		return <div>{this.props.xxx}</div>
	}
}
```

+ 有私有数据

3. 增加`css`

```jsx
render(){
		return <div style={{color:'red'}}>{this.props.xxx}</div>
	}
```

+ 可以抽离为单独的`style.js`的文件，内嵌`style`
+ 样式表`css目录` 
  1. 安装`style-loader`,`css-loader`,
  2. 配置`webpack.config.js` ,`className=`
  3. `css`全局生效,`loader`启用模块化，只能在`类`和`id`使用

```
{test:/\.css$/,use:['style-laoder','css-loader?modules&localIdentName=[path][name]-[local]-[hash:5]']} //参数modules 启用模块化,localIdentName=[path]-[name] 定义类名
:global(.class){},全局，不会被模块化
```

4. 使用第三方`css`,`bootstrap`

+ 字体文件`{test:/\.ttf|woff|woff2|eot|svg$/,use:'url-loader'}`，`npm install url-loader -D`,`npm install file-loader -D`
+ className={[bootstrap.btn,].}

5. 处理css的方法

   1. 将自定义的`css`改为`scss`或者`less`

   2. `scss`模块处理，第三方的不做模块化处理，在使用时直接引用

      ```test: /\.scss$/,use:['style-loader','css-loader?modules&localIdentName=[path][name]-[local]-[hash:5','sass-loader']```

   3. 安装`less`，`scss`,`npm install sass-loader node-sass -D`

6. 安装prop-types校验`npm install prop-types`

7. 

#### 事件

```
setState()
```

#### 数据绑定

1. 通过e

```
this.setState({ myname:e.target.value})
```



2. 通过ref

```
<input type='text' value={this.state.myname} onChange={(e)=>this.changeText(e)} ref="text"></input>
```

3. `this`绑定通过`bind()`

```
//方式1
render(){
	<div onClick={this.handler.bind(this,p1,p2)}> </div>

}
//方式2
constructor(){
//将原函数替换为bind之后的函数，才能将this改变为component
 this.handler=this.hander.bind(this,p1,p2)
}

handler(p1,p2){

}
```

4. `context`共享

```
//固定名字的 共享数据
getChildContext(){
	return {}
}
//固定名字的 数据校验
static childContentTypes={
	
}

//子组件 数据类型校验
static contenTypes={}
//获取共享数据
this.context
```



#### 组件的生命周期 



#### 路由

#### react-router

1. 安装`npm install react-router-dom`,导入 `import {HashRouter,Route,Link} from 'react-router-dom'`
2. HashRouter 一个网站只需要一个
   + `<Hashrouter></Hashrouter>`启用路由
   + 只能有一个跟节点
3. Route
   + path 匹配的路径
   + componet 展示的组件
   + 组件放置在route中
   + 精确匹配，需要增加 exact
   + 匹配参数使用 `：`，通过`props.match.params`获取参数

4. Link <router-Link>
5. `<Switch>`只匹配第一个

#### Ant Design

1. 安装
2. 按需导入`[{"import",{libraryName:"antd",style:"css"}}]`,去掉`css`的导入



#### 结构

1. 根组件`app.jsx`
2. 入口`index.jsx`
3. `fetch`获取数据

```
fecth(url).then(response=>{
	return response.json()
}).then(data=>{

})
```



#### react-redux

1. `action`

   + 必须有`type`
   + 带有state
   + 通过函数生成

2. `reducer`

   + 处理`action`,更新state
   + 返回一个新的state
   + 纯函数

3. `store`

   + 全局一个
   + `subscribe`获取更新之后的state
   + getState
   + subscribe
   + dispatch

4. 流程

   1. 创建`Action`
   2. 调用`store.dispatch(action)`
   3. `构建reducer`的函数处理`action`
   4. 在组件订阅。调用`store.getState()`获取最新数据，通过组件的`setState()`刷新组件

   ```
   componentDidMount(){
           store.subscribe(()=>{
               const s=store.getState()
               console.log(s)
               this.setState({value:s.value})
           })
       }
   ```

#### react-redux

1. `Provider`容器组件，最外层
2. `connect`
3. 流程

   + reducer：处理action与store
+ action ：把数据从ui传送到sotre的唯一有效载荷
   + store：保存所有数据
   + provider：包裹整个结构，配合connect 
   + connect：connect()(component)

