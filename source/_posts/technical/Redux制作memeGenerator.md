---
title: Redux+API制作meme generator
date: 2019-05-14 08:27:51
category: ["前端","React"]
tags: ["React"]
comments:
---

# 环境配置 #

新建项目`create-react-app redux-meme-generator`

安装插件`npm i -S redux react-redux redux-thunk react-bootstrap`

<!--more-->

# 文件结构 #

运行项目`npm run start`，清空`src`下的文件，建立`index.js`，引入`react`和`react-dom`。并在`src`下新建`component`、`actions`、`reducer`文件夹。

**src/index.js**

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './component/App';

import {createStore, applyMiddleware} from 'redux';
import rootReducer from './reducer';
import {Provider} from 'react-redux';
import thunk from 'redux-thunk';

import {fetchMemes} from "./actions";

const store = createStore(rootReducer, applyMiddleware(thunk));
store.subscribe(() => console.log('store', store.getState()));
store.dispatch(fetchMemes());

ReactDOM.render(
  <Provider store={store}>
    <App/>
  </Provider>
  , document.getElementById('root'));
```

**component/App.js**

```javascript
import React, {Component} from 'react';
import {connect} from 'react-redux';

class App extends Component {
  render() {
    return (
      <div>
        <h1>Welcome to the Meme Generator!</h1>
      </div>
    )
  }
}

function mapStateToProps(state) {
  return state;
}

export default connect(mapStateToProps, null)(App);
```
通过以上代码就可以有权限从`component`通过`store`取得`memes`，现在可以进行UI操作。

环境设置完毕。

# Fetch Memes Asyncchronously #

在串接API时需要登录账号密码，我们将这组账号密码封装成一个`action`。

**src/actions/secrets.js**

```javascript
const username = 'AnnieTsai';
const password = '';

export { username, password };
```

但我们不想在项目公开时，被其他人看到我们的账号密码。因此可以到`.gitignore`里将这个`action`的路径写上`src/actions/secrets.js`，就不会发布出去。

**actions/index.js**，编写从`json`获取`memes`的逻辑。

```javascript
export const RECRIVE_MEMES = 'RESEIVE_MEMES';

function receiveMemes(json) {
  const {memes} = json.data;
  return {
    type: RECRIVE_MEMES,
    memes
  }
}

function fetchMemesJson() {
  return fetch('https://api.imgflip.com/get_memes')
    .then(response => response.json())
}

export function fetchMemes() {
  return function (dispatch) {
    return fetchMemesJson()
      .then(json => dispatch(receiveMemes(json)))
  }
}
```

我们可以通过`fetch`来获得所需要的内容。

> Fetch API提供了一个JavaScript接口，用于访问和操作HTTP管道的部分，例如请求和响应。它还提供了一个全局`fetch()`方法，该方法提供了一种简单、合乎逻辑的方式来跨网络异步获取资源。

# 套用thunk middileware #

**reducer/index.js**

```javascript
import {combineReducers} from 'redux';
import {RECRIVE_MEMES} from "../actions";

function memes(state = [], action) {
  switch (action.type) {
    case RECRIVE_MEMES:
      return action.memes;
    default:
      return state;
  }
}

const rootReducer = combineReducers({memes});

export default rootReducer;
```

# Listing memes #

我们可以借由`meme name`来区分每一个`component`，每一个`meme`对象都有`name`属性值，让它们能够被识别。另外，我们也需要加上`key`来判别每个对象的唯一性。

```javascript
      <div>
        <h2>Welcome to the Meme Generator!</h2>
        {
          this.props.memes.map((meme, index) => {
            return (
              <h4 key={index}>{meme.name}</h4>
            )
          })
        }
      </div>
```

# Load more #

当一个页面有大量的资料时，我们就会进行分页或是浓缩的动作。

通过`constructor`建立一个设定显示数量的`state`。

**src/component/App.js**

```javascript
constructor(){
  super();

  this.state = {
    memeLimit: 10
  }
}
```

JavaScript的`slice()`让我们可以从某个字符串`string.slice()`或数组`Array.slice()`提取某一段信息。在渲染的地方加上：`slice(0,this,state,memeLimit)`。

```javascript
this.props.memes.slice(3, this.state.memeLimit).map((meme,index) => {
//设置为3，该从第4个开始提取，只会显示后面7个
    return (
      <h4 key={index}>{meme.name}</h4>
    )
  })
```

接下来我要制作一个按钮，让使用者可以点击`load more`，就可以显示更多`memes`。当使用者点击这个按钮时，便更新`state`，把`memeLimit`再加上10。

```javascript
<div onClick={() => {
     this.setState({memeLimit: this.state.memeLimit+10})
}}>Load 10 more memes...</div>
```

# create meme items #

现在把图片呈现出来

**component/MemeItem.js**

```javascript
import React, {Component} from 'react';

class MemeItem extends Component {
  render() {
    return (
      <div>
        <img
          src={this.props.meme.url}
          alt={this.props.meme.name}
        />
        <p>
          {this.props.meme.name}
        </p>
      </div>
    )
  }
}

export default MemeItem;
```

在`App.js`引入`MemeItem.js`，并在原本渲染呈现`meme name`的地方

转换成`MemeItem`component tag

```javascript
<MemeItem key={index} meme={meme} />
```

# Animating Memes Items #

要实现鼠标移动图片之上有动画，可以通过`css`的`hover`，我们可以通过`setState`不断地更新`hover`的状态。在`MemeItem`component中设置`constructor`

```javascript
constructor(){
  super();

  this.state = {
    hovered: false
  }
}
```






