# redux



**简介**

* 专注于状态管理的库 和 react 解耦
* 单一状态 单向数据流
* 核心概念: 
  * store
  * state
  * action 
  * reducer

**主要功能**

* 首先通过 reducer 新建 store 随时通过 store.getState 获取状态
* 需要状态变更 store, dispatch\(action\) 来修改状态
* Reducer 函数接受 state action 返回新的 state 可以用 store.subscribe 监听每次修改

```text
yarn add redux
```

```text
import { createStore } from 'redux'

// reducer
const counter = (state=0, action) => {
  switch(action.type){
    case 'add':
      return state + 1
    case 'reduce':
      return state - 1
    default:
      return 10
  }
}

// 创建 store
const store = createStore(counter)
const init = store.getState()
console.log(init) // 10

const listener = () => {
  const current = store.getState()
  console.log(`现在有${current}把机关枪`)
}

// 每次状态变化 均会触发 listener 函数
store.subscribe(listener)

// 派发事件 传递 action
store.dispatch({type: 'add'})
store.dispatch({type: 'add'})
store.dispatch({type: 'reduce'})
```



![](../.gitbook/assets/image.png)

**redux 结合 react 使用**

* 把 store.dispatch 方法传递给组件 内部可以调用修改状态
* Subscribe 订阅 render 函数 每次修改都重新渲染
* Redux 相关内容 移到单独的文件 index.redux.js 单独管理



**redux 进阶**

* redux 处理异步 
  * redux-thunk
  * 使用 applyMiddleware 开启 thunk 中间件
  * action 可以返回函数 使用 dispatch 提交 action 

```text
export const addGunAsync = () => {
  return dispatch => {
    setTimeout(() => {
      dispatch(addGUN())
    }, 2000)
  }
}
```



* redux 调试工具
  * Redux DevTools \(chrome shop\)

```text
import {createStore, applyMiddleware, compose} from 'redux'
import thunk from 'redux-thunk'

const store = createStore(counter, compose(
  applyMiddleware(thunk),
  window.devToolsExtension?window.devToolsExtension():()=>{}
))
```

* 使用 react-redux 链接 redux react
  * Provider 组件在应用最外层 传入 store 即可 只用一次
  * Connect 负责从外部获取组件需要的参数
  * Connect 可以用装饰器的方式写
    * npm run eject
    * yarn add babel-plugin-transform-decorators-legacy
    * package.json 里 babel 加上 plugins 配置    

```text
ReactDOM.render(
  (<Provider store={store}>
    <App/>
  </Provider>),
  document.getElementById('root')
)
```

```text
import React from 'react'
import {Button, List} from 'antd-mobile';
import {connect} from 'react-redux'

import { addGUN, removeGUN, addGunAsync } from './index.redux'

class App extends React.Component {
  render() {
    const boss = '李云龙'
    
    return (
      <div>
        <h2>独立团，团长{boss}</h2>
        <OneCamp camper='张大喵'></OneCamp>
        <Cavalry boss="孙德胜"></Cavalry>
        <h1>现在有机枪{this.props.num}把</h1>
        <Button onClick={this.props.addGUN}>申请武器</Button>
        <Button onClick={this.props.removeGUN}>回收武器</Button>
        <Button onClick={this.props.addGunAsync}>延时申请</Button>
      </div>
    )
  }
}

const mapStateToProps = (state) => {
  return {num:state}
}
const actionCreators = {addGUN, removeGUN, addGunAsync}
App = connect(mapStateToProps, actionCreators)(App)
```

