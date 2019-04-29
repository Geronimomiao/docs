# react-router



**简介**

React Router是一组导航组件，它们与您的应用程序以声明方式组合。无论您是希望为Web应用程序设置可收藏的URL还是在React Native中导航的可组合方式，React Router都可以在React渲染的任何地方工作

**安装**

> yarn add react-router-dom

**组件**

* 入门组件
  * BrowserRouter 包裹整个应用
  * Router 路由对应渲染组件 可嵌套
  * Link 跳转专用

```text
import { BrowserRouter, Route } from 'react-router-dom'

const PrimaryLayout = () => (
  <div className="primary-layout">
    <header>
      Our React Router 4 App
    </header>
    <main>
      <Route path="/" exact component={HomePage} />
      <Route path="/users" component={UsersPage} />
    </main>
  </div>
)

const HomePage =() => <div>Home Page</div>
const UsersPage = () => <div>Users Page</div>

const App = () => (
  <BrowserRouter>
    <PrimaryLayout />
  </BrowserRouter>
)

render(<App />, document.getElementById('root'))

作者：undead25
链接：https://juejin.im/post/5995a2506fb9a0249975a1a4
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

* 其他组件
  * url 参数 
    * Router 组件参数可以用冒号表识参数
  * Redirect 组件 
    * 跳转 类似重定向 
  * Switch
    * 只渲染命中的第一个 Route 组件

