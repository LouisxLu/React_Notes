# React_Notes
Notes from learning React.js (Language: Chinese &amp; English mixed)
# React介绍

react是一个用于构建用户**界面**的 JavaScript 库

### React 特点

1. 声明式UI
    1. 声明式对应的是命令式，声明式关注的是what，命令式关注的是how
2. **组件化**
    
    ```
    + 组件是react中**最重要**的内容
    + 组件用于表示页面中的部分内容
    + 组合、复用多个组件，就可以实现完整的页面功能
    ```
    
3. 学习一次，随处使用
    
    ```markdown
    + 使用react/rect-dom可以开发Web应用
    + 使用react/react-native可以开发移动端原生应用（react-native）  RN   安卓 和 ios应用    flutter
    + 使用react可以开发VR（虚拟现实）应用（react360）
    ```
    

## React 脚手架（CLI）

- 脚手架：为了保证各施工过程顺利进行而搭设的工作平台

**使用 React 脚手架创建项目**

- 命令：`npx create-react-app react-basic`
    - npx create-react-app 是固定命令，`create-react-app` 是 React 脚手架的名称
    - react-basic 表示项目名称，可以修改
- 启动项目：`yarn start` or `npm start`
- `npx` 是 npm v5.2 版本(`npm -v`查看)新添加的命令，用来简化 npm 中工具包的使用
    - 原始：1 全局安装`npm i -g create-react-app` 2 在通过脚手架的命令来创建 React 项目
    - ⭐现在：npx 调用**最新的** `npx create-react-app` 直接创建 React 项目

**项目目录结构说明和调整**

- 说明：
    - `src` 目录是我们写代码进行项目开发的目录
    - 查看 `package.json` 两个核心库：`react`、`react-dom`（脚手架已经帮我们安装好，我们直接用即可）
- 调整：
    1. 删除 src 目录下的所有文件
    2. 创建 index.js 文件作为项目的入口文件，在这个文件中写 React 代码即可

## React 的基本使用

### 基本步骤

1. 导入react和react-dom
    
    ```jsx
    import React from 'react'
    import ReactDOM from 'react-dom'
    ```
    
2. 创建react元素
    
    ```jsx
    const title = React.createElement('h1', {id:"box",title:""}, 'hello react')
    //参数1：标签的名字
    //参数2：标签的属性和对象
    //参数3：标签的内容（可以用[]创建多个元素，见练习）
    ```
    
3. 渲染react元素到页面
    
    ```jsx
    ReactDOM.render(title, document.getElementById('root'))
    //参数1：渲染的react元素
    //参数2：需要渲染到哪个容器中
    ```
    

**练习**

使用react，生成以下结构

```jsx
<ul class="list">
    <li>香蕉</li>
    <li>橘子</li>
    <li>苹果</li>
</ul>

//答案:
const title = React.createElement("ul", { id: "box" }, [
  React.createElement("li", null, "香蕉"),
  React.createElement("li", null, "香蕉"),
  React.createElement("li", null, "香蕉"),
]);
ReactDOM.render(title, document.getElementById("root"));
```

# JSX

## 基本使用

`JavaScript XML`的简写，表示了在Javascript代码中写XML(HTML)格式的代码。优势：**声明式**语法更加直观，与HTML结构相同，降低学习成本，提高开发效率。**JSX是react的核心内容**

<aside>
💡 JSX 不是标准的 JS 语法，是 JS 的语法扩展。脚手架中内置的 [@babel/plugin-transform-react-jsx](notion://www.notion.so/@babel/plugin-transform-react-jsx) 包，用来解析该语法。

</aside>

**注意点**

1. 只有在脚手架中才能使用jsx语法
    - 因为JSX需要经过babel的编译处理，才能在浏览器中使用。脚手架中已经默认有了这个配置。
2. JSX必须要有一个根节点
    - `<></>` or `<React.Fragment></React.Fragment>`
3. 没有子节点的元素可以使用`/>`结束
    - 例如：`<br/> <img />`
4. JSX中语法更接近与JavaScript
    - `class` => `className`
    - `for` => `htmlFor`
5. JSX可以换行，如果JSX有多行，推荐使用`()`包裹JSX，防止自动插入分号的bug

**使用prettier插件格式化react代码**

- 安装插件
- 添加prettier的配置
    
    ```jsx
    // 保存的时候使用prettier进行格式化⭐
    "editor.formatOnSave": true,
    // 不要有分号
    "prettier.semi": false,
    // 使用单引号
    "prettier.singleQuote": true,
    // 默认使用prittier作为格式化工具⭐
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    
    ```
    

**嵌入JavaScript表达式**

在jsx中可以在`{}`来使用js表达式（能打印就是表达式）

```jsx
1.基本使用
const name = 'zs'
const age = 18
const title = (
  <h1>
    姓名：{name}, 年龄：{age}
  </h1>
)

2.可以访问对象的属性 {car.brand}
3.可以访问数组的下标 {friends[1]}
4.可以使用三元运算符 {age >= 18? '是':'否'}
5.可以调用方法
6.JSX本身

const span = <span>我是一个span</span>
const title = <h1>盒子{span}</h1>

7.JSX中的注释 {/* 这是jsx中的注释 */}

⚠不要出现语句，比如if for const
```

## 条件渲染

在react中，一切都是javascript，所以条件渲染完全是通过js来控制的

```jsx
1.通过判断if/else控制
const isLoding = false
const loadData = () => {
  if (isLoding) {
    return <div>数据加载中.....</div>
  } else {
    return <div>数据加载完成，此处显示加载后的数据</div>
  }
}

const title = <div>条件渲染：{loadData()}</div>

2.通过三元运算符控制
const isLoding = false
const loadData = () => {
  return isLoding ? (
    <div>数据加载中.....</div>
  ) : (
    <div>数据加载完成，此处显示加载后的数据</div>
  )
}

3.逻辑运算符
const isLoding = false
const loadData = () => {
  return isLoding && <div>加载中...</div>
}

const title = <div>条件渲染：{loadData()}</div>
```

## 列表渲染

我们经常需要遍历一个数组来重复渲染一段结构在react中，通过map方法（见JS数组方法）进行列表的渲染

```jsx
1.列表的渲染
const songs = ['温柔', '倔强', '私奔到月球']
const list = songs.map(song => <li>{song}</li>)
const dv = (
  <div>
    <ul>{list}</ul>
  </div>
)

2.直接在JSX中渲染
<ul>{songs.map(song => <li>{song}</li>)}</ul>

3.key属性的使用（为了提升更新的性能）
const dv = (
  <div>
    <ul>
      {songs.map((song,index) => (
        <li key={index}>{song}</li>
      ))}
    </ul>
  </div>
)

⚠注意：
列表渲染时应该给重复渲染的元素添加key属性，key属性的值要保证唯一
key值避免使用index下标，因为下标会发生改变
```

## 样式处理

### 行内样式-style

```jsx
1.行内样式 style
const dv = (
  <div style={{ color: 'red', backgroundColor: 'pink' }}>style样式</div>
)

2.类名 className
const dv = <div className="title">style样式</div>

//案例:动态控制className
const isRed = true
<h1 className={`${isRed ? "red" : ""} box`}></h1>

//案例2
const isRed = false
const isPink = false
const classArr = ["box"]
if(isRed) classArr.push("red")
if(isPink) classArr.push("pink")
<h1 className={classArr.join(" ")}></h1>

//案例3(了解)
function classNames(obj){
	return Object.keys(obj)
		.filter((key) => obj[key]) //过滤出值为true的属性名
		.join(" ")
}
<h1 className={classNames({ box:true, red:isRed})}></h1>

3.导入样式
import './base.css'
```

**练习**

```jsx
const list = [
  { id: 1, name: "刘德华", content: "给我一杯忘情水" },
  { id: 2, name: "五月天", content: "不打扰，是我的温柔" },
  { id: 3, name: "毛不易", content: "像我这样优秀的人" }
];

//答案
function render() {
  if (list.length === 0) {
    return <div>暂无数据</div>
  }
  return (
    <div>
      <ul>
        {list.map((item) => (+
          <li key={item.id}>
            <h3 className="pink">评论人：{item.name}</h3>
            <p className="skyblue">评论内容：{item.content}</p>
          </li>
        ))}
      </ul>
    </div>
  )
}

ReactDOM.render(render(), document.getElementById('root'))
```

# 组件

- 组件是React中最基本的内容，使用React就是在使用组件
- 组件表示页面中的部分功能
- 多个组件可以实现完整的页面功能
- 组件特点：可复用，独立，可组合

## 创建组件

### 函数组件

使用JS的函数或者箭头函数创建的组件

1. 为了区分普通标签，函数组件的名称必须`大写字母开头`
2. 函数组件`必须有返回值`，表示该组件的结构
3. 如果返回值为null,表示不渲染任何内容

```jsx
1.使用函数创建组件
function Hello () {
    return (
    	<div>这是我的函数组件</div>
    )
}

2.使用箭头函数创建组件
const Hello = () => <div>这是一个函数组件</div>

3.使用组件
ReactDOM.render(<Hello />, document.getElementById('root'))
```

### 类组件

**类与继承**

- 在 ES6 之前通过构造函数创建对象
    
    ```jsx
    function Teacher(name, age){
    	this.name = name
    	this.age = age
    }
    
    Teacher.prototype.sayHi = function(){ //如果都有的方法直接在原型上添加
    	console.log(...)
    }
    
    const stu = new Teacher("xx",xx)
    ```
    
- 在 ES6 中新增了一个关键字 class 类（见JS笔记）和构造函数类似，用于创建对象
- 类与对象的区别
    - 类：指的是一类的事物，是个概念，比如车 手机 水杯等
    - 对象：一个具体的事物，有具体的特征和行为，比如一个手机，我的手机等， **类可以创建出来对象**。
- 类创建对象的基本语法
    - 基本语法`class 类名{}`
    - 构造函数`constructor`的用法，创建对象
    - 在类中提供方法，直接提供即可
    - 在类中不需要使用,分隔

**extends 实现继承**

- extends 基本使用
- 类可以使用它继承的类中所有的成员（属性和方法）
- 类中可以提供自己的属性和方法
- 注意：如果想要给类中新增属性，必须先调用 super 方法

**类组件：使用ES6的class语法创建组件**

1. 类组件的名称必须是大写字母开头
2. 类组件应该继承`React.Component`父类，从而可以使用父类中提供的方法或者属性
3. 类组件必须提供`render`方法，且render方法`必须有返回值`表示该组件的结构
    
    ```jsx
    1.定义组件
    class Hello extends React.Component {
      render() {
        return <div>这是一个类组件</div>
      }
    }
    
    2.使用组件
    ReactDOM.render(<Hello />, document.getElementById('root'))
    ```
    

### 将组件提取到单独的js文件中

组件作为一个独立的个体，一般都会放到一个单独的 JS 文件中

```jsx
实现方式：
1. 创建Hello.js(or jsx)(先在src下创建components文件夹)
2. 创建组件（函数 或 类）
3. 在 Hello.js 中导出该组件

import { Component } from "react"

class Hello extends Component {
	render(){}
}
export default Hello ⭐

4.在 index.js 中导入 Hello 组件

import Hello from "./components/Hello.jsx"

5.渲染组件
```

### 有状态组件和无状态组件

1. 状态（state）即组件的私有数据，当组件的状态发生了改变，页面结构也就发生了改变。
    - 比如计数器案例，点击按钮让数值+1， 0和1就是不同时刻的状态，当状态从0变成1之后，UI也要跟着发生变化。React想要实现这种功能，就需要使用有状态组件来完成。
2. 函数组件又叫做**无状态组件** 函数组件是不能自己提供数据【前提：基于hooks之前说的】
    - 函数组件是没有状态的，只负责页面的展示（静态，不会发生变化）性能比较高
3. 类组件又叫做**有状态组件** 类组件可以自己提供数据，组件内部的状态（数据如果发生了改变，内容会自动的更新）**数据**驱动视图
    - 类组件有自己的状态，负责**更新UI**，只要类组件的数据发生了改变，UI就会发生更新。
4. 在复杂的项目中，一般都是由函数组件和类组件共同配合来完成的。【增加了使用者的负担，所以后来有了hooks】

### 类组件的状态

- 状态`state`即数据，是组件内部的`私有数据`,只有在组件内部可以使用
- `state的值是一个对象`,表示一个组件中可以有多个数据
- state的基本使用
    
    ```jsx
    class Hello extends React.Component {
      constructor() {
        super()
        // 组件通过state提供数据
        this.state = {
          msg: 'hello react'
        }
      }
      render() {
        return <div>state中的数据--{this.state.msg}</div>
      }
    }
    ```
    
- 简洁的语法⭐
    
    ```jsx
    class Hello extends React.Component {
      state = {  //JS自带的语法
        msg: 'hello react'
      }
      render() {
        return <div>state中的数据--{this.state.msg}</div>
      }
    }
    ```
    

# 事件处理

## 注册事件

React注册事件与DOM的事件语法非常像

语法`on+事件名=｛事件处理程序｝` 比如`onClick={this.handleClick}`

注意：**React事件采用驼峰命名法**，比如`onMouseEnter`, `onClick`

```jsx
class App extends React.Component {
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>点我</button> //不要写(),否则就直接调用函数了
      </div>
    )
  }

  handleClick() {
    console.log('点击事件触发了')
  }
}
```

### 事件对象

可以通过事件处理程序的参数获取到事件对象

```jsx
function handleClick(e) {
    e.preventDefault()
    console.log('事件对象', e)
}
<a onClick={this.handleClick}>点我，不会跳转页面</a>
```

### this指向问题

1. 事件处理程序中的this指向的是undefined
2. render方法中的this指向的是当前react组件。
3. **只有事件处理程序中的this有问题**

```jsx
class App extends React.Component {
  state = {
    msg: 'hello react'
  }
  handleClick() {
    console.log(this.state.msg)
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>点我</button>
      </div>
    )
  }
}
```

**this指向问题解决方案**

1. 在render中使用箭头函数。箭头函数的特点：自身没有this，访问的是外部的this
    
    ```jsx
    class App extends React.Component {
      state = {
        msg: 'hello react'
      }
      render() {
        return (
          <div>
            <button onClick={() => this.clickFn()}>点我</button>
          </div>
        )}}
    
    缺点：会把大量的js处理逻辑放到JSX中，将来不容易维护
    ```
    
2. 使用bind将this绑定给render
    
    ```jsx
    class App extends React.Component {
      state = {
        msg: 'hello react'
      }
      handleClick() {
        console.log(this.state.msg)
      }
      render() {
        return (
          <div>
            <button onClick={this.handleClick.bind(this)}>点我</button>
          </div>
        )
      }
    }
    ```
    
3. class实例方法⭐
    
    ```jsx
    class App extends React.Component {
      state = {
        msg: 'hello react'
      }
    
      handleClick = () => {
        console.log(this.state.msg)
      }
      render() {
        return (
          <div>
            <button onClick={this.handleClick}>点我</button>
          </div>
        )
      }
    }
    
    注意：这个语法是试验性的语法，但是有babel的转义，所以没有任何问题
    ```
    

### setState修改状态

- 语法`this.setState({要修改的数据})`
- 注意：不要直接修改state中的值，必须通过`this.setState()`方法（从component从继承而来）进行修改
- `setState`的作用
    - 修改state
    - 更新UI
- 思想：数据驱动视图
    
    ```jsx
    class App extends React.Component {
      state = {
        count: 1
      }
      handleClick() {
        this.setState({
          count: this.state.count + 1 //不能用++，因为会直接修改数据。
        })
      }
      render() {
        return (
          <div>
            <p>次数: {this.state.count}</p>
            <button onClick={this.handleClick.bind(this)}>点我+1</button>
          </div>
        )
      }
    }
    ```
    
- react中核心理念：**状态不可变**
    - 不要直接修改react中state的值，而是提供新的值
    - 直接修改react中state的值，组件并不会更新
    
    ```jsx
    state = {
      count: 0,
      list: []
    }
    // 直接修改值的操作
    this.state.count++
    this.state.list.push('a')
    
    // 创建新的值的操作
    this.setState({
        count: this.state.count + 1,
        list: [...this.state.list, 'b']
    })
    ```
    

# 表单处理

我们在开发过程中，经常需要操作表单元素，比如获取表单的值或者是设置表单的值。

## 受控组件

- HTML中表单元素是可输入的，即表单用户并维护着自己的可变状态（value）。
- 但是在react中，可变状态通常是保存在state中的，并且要求状态只能通过`setState`进行修改。
- React中将state中的数据与表单元素的value值绑定到了一起，`由state的值来控制表单元素的值`
- 受控组件：**value值受到了react控制的表单元素**

**使用步骤**

1. 在state中添加一个状态，作为表单元素的value值（控制表单元素的值）
2. 给表单元素添加`change`事件，设置state的值为表单元素的值（控制值的变化）
    
    ```jsx
    class App extends React.Component {
      state = {
        msg: 'hello react'
      }
    
      handleChange = (e) => {
        this.setState({
          msg: e.target.value //e.target 代表当前触发事件的DOM元素
        })
      }
    
      render() {
        return (
          <div>
            <input type="text" value={this.state.msg} onChange={this.handleChange}/>
          </div>
        )
      }
    }
    ```
    

### 常见的受控组件

- 文本框、文本域、下拉框（操作value属性）
- 复选框（操作checked属性）
    
    ```jsx
    class App extends React.Component {
      state = {
        usernmae: '',
        desc: '',
        city: "2",
        isSingle: true
      }
    
      handleName = e => {
        this.setState({
          name: e.target.value
        })
      }
      handleDesc = e => {
        this.setState({
          desc: e.target.value
        })
      }
      handleCity = e => {
        this.setState({
          city: e.target.value
        })
      }
      handleSingle = e => {
        this.setState({
          isSingle: e.target.checked
        })
      }
    
      render() {
        return (
          <div>
            姓名：<input type="text" value={this.state.username} onChange={this.handleName}/>
            <br/>
            描述：<textarea value={this.state.desc} onChange={this.handleDesc}></textarea>
            <br/>
            城市：<select value={this.state.city} onChange={this.handleCity}>
              <option value="1">北京</option>
              <option value="2">上海</option>
              <option value="3">广州</option>
              <option value="4">深圳</option>
            </select>
            <br/>
            是否单身：<input type="checkbox" checked={this.state.isSingle} onChange={this.handleSingle}/>
          </div>
        )
      }
    }
    ```
    

### 多表单元素的优化

问题：每个表单元素都需要一个单独的事件处理程序，处理太繁琐

优化：使用一个事件处理程序处理多个表单元素

步骤

- 给表单元素添加name属性，名称与state属性名相同
- 根据表单元素类型获取对应的值
- 在事件处理程序中通过`[name]`修改对应的state
    
    ```jsx
    class App extends React.Component {
      state = {
        username: '',
        desc: '',
        city: "2",
        isSingle: true
      }
    
      handleChange = (e) => {
        let {name, type, value, checked} = e.target //es6中的对象解构
        value = type === 'checkbox' ? checked : value
        this.setState({
          [name]: value //es6中的属性名表达式
        })
      }
      render() {
        return (
          <div>
            姓名：<input type="text" name="username" value={this.state.username} onChange={this.handleChange}/>
            <br/>
            描述：<textarea name="desc" value={this.state.desc} onChange={this.handleChange}></textarea>
            <br/>
            城市：<select name="city" value={this.state.city} onChange={this.handleChange}>
              <option value="1">北京</option>
              <option value="2">上海</option>
              <option value="3">广州</option>
              <option value="4">深圳</option>
            </select>
            <br/>
            是否单身：<input type="checkbox" name="isSingle" checked={this.state.isSingle} onChange={this.handleChange}/>
          </div>
        )
      }
    }
    
    ```
    

## 非受控组件

非受控组件借助于ref，使用原生DOM的方式来获取表单元素的值

**使用步骤**

```jsx
1.调用React.createRef()方法创建一个ref

constructor() {
  super()
  this.txtRef = React.createRef()
}
txtRef = React.createRef()

2.将创建好的ref对象添加到文本框中

<input type="text" ref={this.txtRef}/>

3.通过ref对象获取文本框的值

handleClick = () => {
  console.log(this.txtRef.current.value)
}

*非受控组件用的不多，推荐使用受控组件 
```

### 综合案例

[评论列表案例](https://www.notion.so/0124175fd4904ad29ac3caf421e8afbd)

# 组件通讯

<aside>
💡 **组件**是独立且封闭的单元，默认情况下，只能使用组件自己的数据。在组件化过程中，我们将一个完整的功能拆分成多个组件，以更好的完成整个应用的功能。而在这个过程中，多个组件之间不可避免的要**共享某些数据**。为了实现这些功能，就需要打破组件的独立封闭性，让其与外界沟通。这个过程就是**组件通讯**。

</aside>

## PROPS

- 组件是封闭的，要接收外部数据应该通过props来实现
- **props的作用：接收传递给组件的数据**
- 传递数据：给组件标签添加属性
- 接收数据：函数组件通过参数props接收数据，类组件通过this.props接收数据

### 函数组件通讯

```jsx
1.子组件

export default function Hello(props) {
    console.log(props)
    return (
    	<div>接收到数据：{props.name}</div>
    )
}

//可以用解构的方式写
export default function Hello({name, age}) {

2.父组件

<Hello name="jack" age={19} />  //写数字要加{}
```

### 类组件通讯

```jsx
1.子组件

class Hello extends React.Component {
    render() {
        return (
        	<div>接收到的数据：{this.props.age}</div>
        )
    }
}
//也可以用解构的方式写
const {car, money, check} = this.props

2.父组件

<Hello name="jack" age={19} />
```

### props的特点

1. 可以给组件传递任意类型的数据
2. props是只读的，不允许修改props的数据 （单向数据流：父组件传递给子组件）
3. 注意：在类组件`constructor`中使用的时候，**需要把props传递给super()**，否则构造函数无法获取到props
    
    ```jsx
    class Hello extends React.Component {
        constructor(props) {
            // 推荐将props传递给父类构造函数
            super(props)
        }
        render() {
        	return <div>接收到的数据：{this.props.age}</div>
        }
    }
    ```
    

### 组件通讯三种方式

1. 父传子
    1. 父组件提供要传递的state数据
    2. 给子组件标签添加属性，值为 state 中的数据
    3. 子组件中通过 props 接收父组件中传递的数据
    
    ```jsx
    1.父组件提供数据并且传递给子组件
    
    class Parent extends React.Component {
        state = { lastName: '王' }
        render() {
            return (
                <div>
                    传递数据给子组件：<Child name={this.state.lastName} />
                </div>
            )
        }
    }
    
    2.子组件接收数据
    
    function Child(props) {
    	return <div>子组件接收到数据：{props.name}</div>
    }
    ```
    
2. 子传父
    1. 思路：利用回调函数，父组件提供回调，子组件调用，将要传递的数据作为回调函数的参数。
    2. 父组件提供一个回调函数（用于接收数据）
    3. 将该函数作为属性的值，传递给子组件
    4. 子组件通过 props 调用回调函数
    5. 将子组件的数据作为参数传递给回调函数
    
    ```jsx
    1.父组件提供函数并且传递给字符串、
    
    class Parent extends React.Component {
        getChildMsg = (msg) => {
            console.log('接收到子组件数据', msg)
        }
        render() {
            return (
                <div>
                	子组件：<Child getMsg={this.getChildMsg} />
                </div>
            )
        }
    }
    
    2.子组件接收函数并且调用
    
    class Child extends React.Component {
        state = { childMsg: 'React' }
        handleClick = () => {
        	this.props.getMsg(this.state.childMsg)
        }
        return (
        	<button onClick={this.handleClick}>点我，给父组件传递数据</button>
        )
    }
    
    ***注意：回调函数中 this 指向问题！**
    ```
    
3. 兄弟父子
    
    ```
    - 将共享状态提升到最近的公共父组件中，由公共父组件管理这个状态
    - 思想：**状态提升**
    - 公共父组件职责：
        - 提供共享状态
        - 提供操作共享状态的方法
    - 要通讯的子组件只需通过 props 接收状态或操作状态的方法
    ```
    

### 组件通讯-context

**基本概念**

由于使用 props 一层层组件往下传递过于繁琐，所以可以使用 Context 组件通讯。（后期Redux）

**作用**：跨组件传递数据（比如：主题、语言等）

**实现思路**

```jsx
1.调用React. createContext() 创建 Provider（提供数据）和 Consumer（消费数据） 两个组件(在父组件中)

const { Provider, Consumer } = React.createContext()
export { Consumer}

2.使用 Provider 组件作为父节点。

render(){
	return(
		<Provider>
		    <div className="App">
		    	<Child1 />
		    </div>
		</Provider>
	)
}

3.设置 value 属性，表示要传递的数据。

<Provider value="pink"> or <Provider value={this.state.color}> 将数据写在state里

4.调用 Consumer 组件接收数据

import { Consumer } from "./index"

<Consumer>
	{(data) => <span>data参数表示接收到的数据{data}</span>}
</Consumer>

*consumer包含的必须是函数
```

## Props深入

### children属性

```jsx
children属性：表示该组件的子节点，只要组件有子节点，props就有该属性
children属性与普通的props一样，值可以是任意值（文本、React元素、组件，甚至是函数）
只不过内容可以写在中间

function Hello(props) {
  return (
    <div>
      该组件的子节点：{props.children} //props.children 的内容是：我是子节点
    </div>
  )
}

<Hello>我是子节点</Hello>

*只能有一个children
```

### props校验

目的：校验接收的props的数据类型，增加组件的健壮性

对于组件来说，props是外来的，无法保证组件使用者传入什么格式的数据

如果传入的数据格式不对，可能会导致组件内部报错。**组件的使用者不能很明确的知道错误的原因。**

props校验允许在创建组件的时候，就约定props的格式、类型等

作用：规定接收的props的类型必须为数组，如果不是数组就会报错，增加组件的健壮性。

**使用步骤**

```jsx
1. 导入 prop-types 包
2. 使用组件名.propTypes = {} 来给组件的props添加校验规则
3. 校验规则通过 PropTypes 对象来指定

import PropTypes from 'prop-types'
function App(props) {
    return (
    	<h1>Hi, {props.colors}</h1>
    )
}
App.propTypes = {
    // 约定colors属性为array类型
    // 如果类型不对，则报出明确错误，便于分析错误原因
    colors: PropTypes.array
}

```

**约束规则（了解 / TS再回顾）**

```jsx
1. 常见类型：array、bool、func、number、object、string
2. React元素类型：element
3. 必填项：isRequired
4. 特定结构的对象：用 shape({ })方法

// 常见类型
optionalFunc: PropTypes.func,
// 必选
requiredFunc: PropTypes.func.isRequired,
// 特定结构的对象
optionalObjectWithShape: PropTypes.shape({
	color: PropTypes.string,
	fontSize: PropTypes.number
})

```

### props默认值

```jsx
场景：分页组件  每页显示条数
作用：给 props 设置默认值，在未传入 props 时生效

function App(props) {
    return (
        <div>
            此处展示props的默认值：{props.pageSize}
        </div>
    )
}
// 设置默认值
App.defaultProps = {
	pageSize: 10
}
// 不传入pageSize属性
<App />

```

### 类的静态属性static（详见JS）

```jsx
- 实例成员: 通过实例调用的属性或者方法叫做实例成员（属性或者方法）
- 静态成员：通过类或者构造函数本身才能访问的属性或者方法

class Person {
   name = 'zs',
   static age = 18
   sayHi() {
       console.log('哈哈')
   }
   static goodBye() {
       console.log('byebye')
   }
}

const p = new Person()

console.log(p.name) //实例成员
p.sayHi()

console.log(Person.age) //静态成员
Person.goodBye()

```

# 生命周期（待看）

**概述**

- 组件的生命周期有助于理解组件的运行方式、完成更复杂的组件功能、分析组件错误原因等
- 组件的生命周期：组件从被创建到挂载到页面中运行，再到组件不用时卸载的过程
- 钩子函数的作用：为开发人员在不同阶段操作组件提供了时机。
- **只有 类组件 才有生命周期。**

**生命周期的整体说明**

- 每个阶段的执行时机
- 每个阶段钩子函数的执行顺序
- 每个阶段钩子函数的作用

![详见：[http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d106a0e6-7bc1-4ba3-bec2-0a36a0a2449e/Untitled.png)

详见：[http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

**挂载阶段**

执行时机：组件创建时（页面加载时）

执行顺序：

**更新阶段**

- 执行时机：1. setState() 2. forceUpdate() 3. 组件接收到新的props
- 说明：以上三者任意一种变化，组件就会重新渲染
- 执行顺序

**卸载阶段**

- 执行时机：组件从页面中消失
