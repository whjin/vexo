---
title: React项目详解
date: 2019-04-09 20:02:01
category: ["前端"]
tags: ["React"]
comments:
---

# React项目指导 #

## 使用`webpack`需要安装的依赖 ##

<!--more-->

1. `webpack`，`webpack-cli`，`react`，`react-dom`
2. `babel-loader`，`@babel/core`，`@babel/preset-env`，`@babel/preset-react`
3. 设置`.babelrc`，`{"presets": ["@babel/preset-env","@babel/preset-react"]}`
4. 设置`scripts`：
   
     ```javascript
    "dev": "webpack --mode development",
    "build": "webpack --mode production"
    ```
5. 设置`webpack-dev-server`：   
    
    ```javascript
    devServer: {
      compress: true,
        port: 9000，
        hot: true
    },

    "start": "webpack-dev-server --config webpack.config.js" 
    ```
6. 设置`performance`：

    ```javascript
    performance: {
      hints: false
    }
    ```

## `Component` ##

1. 基本组件

    ```javascript
    let title = <h1>Hello, world!</h1>
    
    ReactDOM.render(title,document.getElementById('root'))
    ```

2. 动态组件

    ```javascript
    import React from 'react';
    import ReactDOM from 'react-dom';
    
    let displayTime = () => {
      let nowTime = (
        <div>
          <span>现在时间：{new Date().toLocaleTimeString()}</span>
        </div>
      );
      ReactDOM.render(t
        nowTime,
        document.getElementById('root')
      );
    };
    
    setInterval(displayTime, 1000);
    ```

3. `class`组件构建器

    ```javascript
    import React, {Component} from 'react';
    import ReactDOM from 'react-dom';
    
    class HelloTitle extends Component {
      render() {
        return <h1>Hello,World!</h1>
      }
    }
    
    ReactDOM.render(
      <HelloTitle/>,
      document.getElementById('root')
    );
    ```

4. `props`属性

    ```javascript
    import React, {Component} from 'react';
    import ReactDOM from 'react-dom';
    
    class HelloTitle extends Component {
      render() {
        return <h1>Hello,{this.props.name}!</h1>
      }
    }
    
    let titleDiv = (
      <div>
        <HelloTitle name="React"/>
        <HelloTitle name="World"/>
      </div>
    );
    
    ReactDOM.render(
      titleDiv,
      document.getElementById('root')
    );
    ```

5. `props`多层使用

    ```javascript
    import React, {Component} from 'react';
    import ReactDOM from 'react-dom';
    
    class HelloTitle extends Component {
      render() {
        return <h1>Hello,{this.props.name}!</h1>
      }
    }
    
    class HelloDiv extends Component {
      render() {
        return <div><HelloTitle name={this.props.name}/></div>
      }
    }
    
    ReactDOM.render(
      <HelloDiv name="React"/>,
      document.getElementById('root')
    );
    ```

6. 组件复用

    ```javascript
    import React, {Component} from 'react';
    import ReactDOM from 'react-dom';
    
    class HelloTitle extends Component {
      render() {
        return <h1 style={this.props.style}>{this.props.content}</h1>
      }
    }
    
    class HelloDiv extends Component {
      render() {
        return <div>
          <HelloTitle content="比较大的字" style={{'fontSize': 18}}/>
          <HelloTitle content="比较小的字" style={{'fontSize': 12}}/>
        </div>
      }
    }
    
    ReactDOM.render(
      <HelloDiv/>,
      document.getElementById('root')
    );
    ```

## `Component`的状态`state`和生命周期 ##

### `state`属性 ###

```javascript
constructor(props) {
  super(props);
  this.state = {
    time: new Date().toLocaleTimeString()
  }
}

render() {
  return <h1>现在时间是{this.state.time}</h1>
}
```

组件构建完成后先执行的动作，`componentDidMount()`：

```javascript
componentDidMount() {
  let upTime = () => {
    this.setState({time: new Date().toLocaleTimeString()})
  };
  setInterval(upTime, 1000)
}
```

### `setState()`修改状态值 ###

```javascript
this.setState({time: new Date().toLocaleTimeString()})
```

### 生命周期 ###

1. 在`constructor`中初始化组件内部的资料。
2. 使用`render()`在网页上输出组件内容。
3. 输出后会执行`componentDidMount()`进行一次调用。
4. 当组件内部的`state`值被修改时执行`componentDidUpdate()`。
5. 当组件被移除时会执行`componentWillUnmount()`的内容一次。

**`componentDidMount()`**

1. Component已经`render`到实体DOM阶段完成的时候触发；
2. 此`method`只会被呼叫一次；
3. 在这裡可以`setState()`，并会再次重新`render`、`component`一次；
4. 可以放入具有`side effect`的`function`，如`setInterval`、呼叫API等等。

**`componentWillUnmount()`**

1.  Component即将从实体DOM阶段移除「之前」的时候触发；
2.  也是只会被呼叫一次；
3.  不可以在这裡使用`setState()`；
4.  也可以放入具有`side effect`的`function`。

```javascript
class Clock extends Component {
  constructor(props) {
    super(props);
    this.state = {
      currentTime: new Date().toLocaleString()
    }
  }

  componentDidMount() {
    this.timer = setInterval(this.updateTime, 1000)
  }

  componentWillUnmount() {
    clearInterval(this.timer)
  }

  updateTime = () => {
    this.setState({
      currentTime: new Date().toLocaleString()
    })
  };

  render() {
    const {currentTime} = this.state;
    return (
      <div className="clock">
        <div>{currentTime}</div>
      </div>
    )
  }
}
```

### `component`各阶段的生命周期方法 ###

1. 挂载（`Mounting`）：组件一开始呈现到真实网页的过程

```javascript
class LifeCycle extends Component {
  constructor(props) {
    super(props);
    //  建构式，推进组件初始state设定，绑定方法，接受父级props的地方
    //  只会被调用一次
    //  不适合使用具有side effect的工作，如AJAX调用
  }

  static getDerivedStateFromProps(nextProps, prevState) {
    //  React V16.3新增的生命周期方法
    //  在组件建构之后,render()被调用之前
    //  每次接收新的props后回传object更新state；也可以回传null不做更新
  }

  UNSAFE_componentWillMount() {
    //  即将在React V17中移除，不可与static getDerivedStateFromProps同时出现
    //  在render()调用之后被调用，且之后被调用一次
    //  会用到的地方仅在于服务器端的应用
    //  适合设定初始化数据的地方，不适合做有side effect的工作
  }

  render() {
    //  在class component中「唯一」必要存在的方法
    //  尽量pure，不应该改变component的state
    //  如需要和browser有互动的话，将其放进componentDidMount()中
    return (
      <div></div>
    )
  }

  componentDidMount() {
    //  在render()被调用后，组件已经在真实DOM呈现之后被调用执行
    //  只会被调用一次，适合执行AJAX、计时器设定、加入eventListener等有副作用的工作
    //  调用setState()可能会再执行一次render()
  }
}
```

2. 更新（Updating）：使用者的操作中，组件的状态和属性被改变

```javascript
class LifeCycle extends Component {
  UNSAFE_componentWillReceiveProps(nextProps) {
    //  即将在React V17中移除，不可与static getDerivedStateFromProps同时出现
  }

  static getDerivedStateFromProps(nextProps, prevState) {
    //  React V16.3新增的新生命周期方法
    //  在组件构建之后，render()被调用之前
    //  每次接收新的props后回传object更新state；也可回传null不做更新
    //  搭配componentDidUpdate，可以达到与componentWillReceivedProps的效果
  }

  shouldComponentUpdate() {
    //  让使用者自定义是否进行component更新，预设都会默认更新
    //  只有少部分的情况才会使用此方法，如进行复杂耗时的计算
    //  尽量不要检查太过深层的值，也不适合执行具有side effect的工作
  }

  UNSAFE_componentWillUpdate(nextProps, nextState) {
    //  即将在React V17中移除，不可与static getDerivedStateFromProps同时出现
    //  在组件即将更新「之前」调用
    //  不能在此使用setState方法，若要改变请用getDerivedStateFromProps
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    //  在render之后，在最新的渲染前输出交给真实DOM前会立即执行
    //  返回的值作为componentDidUpdate的第三个值
    //  搭配componentDidUpdate，可以达到与componentWillUpdate的效果
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    //  会发生在更新「之后」被调用
    //  如果shouldComponentUpdate回传的是false，就不会调用此方法
    //  适合执行具有side effect的地方
  }
}
```

3. 卸载（Unmounting）：组件要移除真实DOM的阶段

```javascript
class LifeCycle extends Component {
  componentWillMount() {
    //  在组件即将要移除真实DOM时会执行
    //  可以在这里做中断网络连接、清楚计时器、移除事件监听器
    //  不适合使用setState方法
  }
}
```

#### `catch error` ####

```javascript
class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = {
      hasError: false
    }
  }

  componentDidCatch(error, info) {
    //  是error handle的方法，与挂载和更新阶段有密切关系
    //  可以用来捕捉子组件的任何JavaScript的错误
    //  可以记录这些错误，或是呈现在目前反馈用的操作界面上
    //  不能在事件的callback上使用

    //  显示在反馈的UI上
    this.setState({hasError: true});
    //  也可以用额外的错误记录服务
    logErrorMyService(error, info);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong...</h1>
    }
    return this.props.children
  }
}
```

上面就是`component`可以使用的生命周期方法，最常用主要是这些：

1. `constructor()`
2. `render()`
3. `componentDidMount()`
4. `compoinentDidUpdate()`
5. `componentWillUnmount()`

## `Component`的事件处理 ##

1. 取得触发事件的DOM

```javascript
class InputGender extends Component {
  constructor(props) {
    super(props);
    this.state = {
      gender: ''
    };
    this.changeGender = this.changeGender.bind(this)
  }

  changeGender(event) {
    console.log(event.target.value);
    this.setState({
      gender: event.target.value
    });
  }

  componentDidUpdate() {
    console.log(`已将state.gender变动为：${this.state.gender}`)
  }

  render() {
    return (
      <select onChange={this.changeGender}>
        <option value="M">男</option>
        <option value="W">女</option>
      </select>
    )
  }
}
```

```javascript
class HelloTitle extends Component {
  render() {
    return <h1>{this.props.title}</h1>
  }
}

{(this.state.gender === 'M') ? <HelloTitle title="先生"/> : <HelloTitle title="女士"/>}
```

### 用绑定的`state`取得输入资料 ###

```javascript
class EasyForm extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name: ""
    };
    this.changeState = this.changeState.bind(this);
    this.submitForm = this.submitForm.bind(this);
  }

  changeState(event) {
    this.setState({
      name: event.target.value,
    });
  }

  submitForm(event) {
    let element = document.querySelector('span');
    element.innerHTML = `${this.state.name}`;
    event.preventDefault()
  }

  render() {
    return (
      <div>
        <form onSubmit={this.submitForm}>
          <label>姓名：</label>
          <input id="name" name="name" onChange={this.changeState} value={this.state.name}/>
          <input type="submit" value="提交" style={{'marginLeft': 6}}/>
        </form>
        <p>现在输入的名字是：<span style={{'color': '#FF7F24'}}></span></p>
      </div>
    )
  }
}
```

### 受控组件 ###

```javascript
class EasyForm extends Component {
  constructor(props) {
    super(props);
    this.state = {
      lists: [
        {id: '01', listName: '写文章', check: false},
        {id: '02', listName: '写代码', check: false},
        {id: '03', listName: '旅游', check: true},
        {id: '04', listName: '踢球', check: true},
        {id: '05', listName: '公益', check: false},
      ]
    };
    this.submitForm = this.submitForm.bind(this);
    this.changeState = this.changeState.bind(this);
  }

  changeState(index) {
    let arrLists = this.state.lists;
    arrLists[index].check ? arrLists[index].check = false : arrLists[index].check = true;
    this.setState({
      lists: arrLists,
    });
  }

  submitForm(event) {
    let status = "目前做了：";
    this.state.lists.map((list) => list.check ? status += `${list.listName} ` : '');
    console.log(status);
    event.preventDefault()
  }

  render() {
    let lists = this.state.lists.map((list, index) => (
      <div key={list.id}>
        <input type="checkbox"
               checked={list.check}
               onChange={this.changeState.bind(this, index)}
               key={list.id}
        />
        <label>{list.listName}</label>
      </div>
    ));
    return (
      <form onSubmit={this.submitForm}>
        <div>
          <label>每日待办清单：</label>
          {lists}
        </div>
        <input type="submit" value="发送表单"/>
      </form>
    )
  }
}
```

### 非受控组件 ###

```javascript
class EasyForm extends Component {
  constructor(props) {
    super(props);
    this.submitForm = this.submitForm.bind(this);
    this.filebox = React.createRef()
  }

  submitForm(event) {
    console.log(`选择文档为：${this.filebox.current.files[0].name}`)
    event.preventDefault()
  }

  render() {
    return (
      <form onSubmit={this.submitForm}>
        <div>
          <label>上传文档：</label>
          <input type="file" ref={this.filebox}/>
        </div>
        <input type="submit" value="送出表单"/>
      </form>
    )
  }
}
```

### `refs`操作DOM ###

```javascript
class App extends Component {
  constructor() {
    super();
    this.state = {
      itemList: []
    };
    this.addFile = React.createRef();
  }

  addItem = () => {
    const {itemList} = this.state;
    const tempList = Object.assign([], itemList);
    if (this.addFile.current.value !== '') {
      tempList.push(this.addFile.current.value);
    }
    this.setState({
      itemList: tempList
    });
    this.addFile.current.value = ''
  };

  render() {
    const {itemList} = this.state;
    return (
      <div className="App">
        <input type="text" name="addFile" ref={this.addFile}/>
        <input type="button" onClick={this.addItem} value="ADD"/>
        <ul className="list">
          {itemList.map((item, index) =>
            <li key={`item_${index}`}>{item}</li>
          )}
        </ul>
      </div>
    );
  }
}
```

# 实例：`TODOLIST` #

**`TodoList.js`**

```javascript
class TodoList extends Component {
  constructor(props) {
    super(props);
    this.state = {
      list: []
    }
  }

  addItem = (text) => {
    const {list} = this.state;
    if (text !== '') {
      const tempArr = list.concat({
        id: list.length + 1,
        text,
        status: false
      });
      this.setState({list: tempArr})
    }
  };

  toggleStatus = (id) => {
    const {list} = this.state;
    const tempArr = list.map(item => {
      if (item.id.toString() === id.toString()) {
        return ({
          id: item.id,
          text: item.text,
          status: !item.status
        })
      }
      return item;
    });
    this.setState({list: tempArr})
  };

  render() {

    const {list} = this.state;
    const divStyle = {
      width: '250px',
      margin: 'auto',
      textAlign: 'left'
    };
    return (
      <div style={divStyle}>
        <TodoForm onAddItem={this.addItem}/>
        <ul>
          {list.map(item => (
            <TodoItem
              key={item.id}
              id={item.id}
              status={item.status}
              onItemClick={this.toggleStatus}
            >
              {item.text}
            </TodoItem>
          ))}
        </ul>
      </div>
    )
  }
}
```

**`TodoForm.js`**

```javascript
class TodoForm extends Component {
  constructor(props) {
    super(props);
    this.inputRef = React.createRef();
  }

  formSubmit = (e) => {
    const {onAddItem} = this.props;
    e.preventDefault();
    onAddItem(this.inputRef.current.value);
    this.inputRef.current.value = ''
  };

  render() {
    return (
      <form onSubmit={this.formSubmit}>
        <input type="text" name="todoItem" ref={this.inputRef} autoComplete="off"/>
        <button type="submit" value="submit">submit</button>
      </form>
    )
  }
}
```

**`TodoItem.js`**

```javascript
class TodoItem extends Component {
  handleItemClick = (e) => {
    const {onItemClick} = this.props;
    onItemClick(e.target.id)
  };

  render() {
    const {children, id, status} = this.props;
    return (
      <li
        id={id}
        onClick={this.handleItemClick}
        data-status={status}
        style={
          status ?
            {textDecoration: 'line-through'} :
            {textDecoration: 'none'}
        }
      >
        {children}
      </li>
    )
  }
}
```