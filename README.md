# react

### 开发环境搭建

1. 安装 node

2. 脚手架安装

> npm install -g create-react-app

3. 创建第一个 react 项目

> create-react-app demo

##### 项目目录介绍

- README.md
  > 这个文件主要作用就是对项目的说明
- package.json
  > webpack 配置和项目包管理文件
- package-lock.json
  > 锁定安装时的版本号
- gitignore
  > 这个是 git 的选择性上传的配置文件
- node_modules
  > 项目的依赖包
- public
  > 公共文件
  - favicon.ico
    > 网站或者说项目的图标
  - index.html
    > 首页的模板文件
  - mainifest.json
    > 移动端配置文件
- src
  > 主要代码编写文件
  - index.js
    > 入口文件
  - index.css
    > index.js 里的 CSS 文件
  - app.js
    > 一个方法模块
  - serviceWorker.js
    > 用于写移动端开发的，PWA 必须用到这个文件，有了这个文件，就相当于有了离线浏览的功能

### 基本示例

> index.js

```js
import React from "react";
import { render } from "react-dom";
import App from "./App.js";

render(<App />, document.getElementById("root"));
```

> App.js

```js
import React, { Component } from "react";

export default class App extends Component {
  render() {
    return <div>hello world!</div>;
  }
}
```

> Fragment 标签讲解（包裹标签专用）

### 简单的 todolist

```js
import React, { Component, Fragment } from "react";

export default class App extends Component {
  // 构造函数
  constructor(props) {
    super(props);
    this.state = {
      inputValue: "dsds",
      list: []
    };
  }
  inputChange(e) {
    this.setState({
      inputValue: e.target.value
    });
  }
  addList() {
    this.setState({
      list: [...this.state.list, this.state.inputValue]
    });
    this.setState({
      inputValue: ""
    });
  }
  delete(key) {
    this.setState({
      list: this.state.list.splice(key, 1)
    });
  }

  render() {
    return (
      <Fragment>
        <div>
          {/* 注释 */}
          <input
            type="text"
            value={this.state.inputValue}
            onChange={this.inputChange.bind(this)}
          />
          <button onClick={this.addList.bind(this)}>Add</button>
          <ul>
            {this.state.list.map((item, key) => {
              return (
                <li key={key}>
                  {item}
                  <button onClick={this.delete.bind(this, key)}>del</button>
                </li>
              );
            })}
          </ul>
        </div>
      </Fragment>
    );
  }
}
```

### jsx 防坑指南

##### 注释

```js
{
  /* 注释 */
}
```

##### class

应该写成 className

##### html 中 label 标签里的 for

应该写成 htmlFor

### 组件拆分

##### 父子组件传值

父组件向子组件传递内容，靠属性的形式传递

##### 子组件调用父组件方法

子组件可以通过 props 中传递的事件响应父组件

### 单项数据流和函数式编程

### 调试工具的安装和使用

react developer tools

### propTypes 校验传递值

```js
import PropTypes from 'prop-types'
......
TodoItem.propTypes = {
  content: PropTypes.string,
  index: PropTypes.number,
  deleteItem: PropTypes.func
}
```

### ref 的使用

> 注意使用 setState 中的第二次参数，来进行异步回调

### 组件的生命周期

> 四个大阶段

1. Initialization:初始化阶段
2. Mounting: 挂在阶段

- componentWillMount : 在组件即将被挂载到页面的时刻执行
- render : 页面 state 或 props 发生变化时执行
- componentDidMount : 组件挂载完成时被执行

3. Updation: 更新阶段

- shouldComponentUpdate 函数会在组件更新之前，自动被执行
- componentWillUpdate---组件更新前，shouldComponentUpdate 函数之后执行
- componentDidUpdate----组件更新之后执行
- componentWillReceiveProps 存于 dom 中且传递数据过来时才执行

4. Unmounting: 销毁阶段

- componentWillUnmount 组件从页面中删除的时候执行

> componentWillMount 和 componentDidMount 这两个生命周期函数，只在页面刷新时执行一次，而 render 函数是只要有 state 和 props 变化就会执行
> componentWillReceiveProps 存于 dom 中且传递数据过来时才执行

### 生命周期 shouldComponentUpdate 改善组件的性能

> shouldComponentUpdate

```js
  // 声明周期
  shouldComponentUpdate(nextProps,nextState){
    if(nextProps.content !== this.props.content){
      return true
    }else{
        return false
    }
    // return false 不执行update
  }
```

### axios 数据请求

```js
npm install axios --save
```

```js
componentDidMount(){
  axios.post('https://web-api.juejin.im/v3/web/wbbr/bgeda')
    .then((res)=>{console.log('axios 获取数据成功:'+JSON.stringify(res))  })
    .catch((error)=>{console.log('axios 获取数据失败'+error)})
}
```

###### EasyMock 网站:https://www.easy-mock.com/

### react 动画 react-transition-group

```js
npm install react-transition-group --save
```
