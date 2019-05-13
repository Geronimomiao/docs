# react-router 基础



**React Router V4**

是对 React Router 一次彻底的重构 采用动态路由 遵循 React 一切皆组件的思想 每一个 Route 都是一个普通的 React 组件

**React Router**

通过 Router Route 两个组件完成路由功能

* Router 
  * BrowserRouter
  * HashRouter
* Route
  * 当URL和Route匹配时 Route会创建一个match作为props中的一个属性传递给被渲染的组件 该对象包含以下4个属性
    * params 匹配从URL中解析的参数
    * isExact URL完全匹配为 true  
    * path 构建嵌套路由会使用到
    * url URL的匹配部分
  * 渲染组件的方式
    * component
    * reder
    * children
* Switch
  * 当URL和多个路由匹配 只让第一个匹配的URL渲染
* exact
  * 完全匹配 Route 才渲染    
* Link 
  * to 可以是String Object 类型
  * object
    * pathname
    * search 
    * hash
    * state 



**除了使用 Link  还可以通过 history 对象实现手动导航**

* history.push\(path, \[state\]\)
* history.replace\(path, \[state\]\)

