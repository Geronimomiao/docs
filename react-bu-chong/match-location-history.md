# match location history



**在 Route 的渲染的组件 props 会自动包含 match location history**

```text
const Three = (prop) => {
  console.log(prop)
  return <h2>Component Three</h2>
}

class Dashboard extends React.Component {
  constructor(props) {
    super(props)
  }

  render() {
    // console.log(this.props)
    return (
      <div>
        <ul>
          <li>
            <Link to='/dashboard/'>Index</Link>
          </li>
          <li>
            <Link to='/dashboard/two'>Two</Link>
          </li>
          <li>
            <Link to='/dashboard/three'>Three</Link>
          </li>
        </ul>
        <Route path='/dashboard/' exact component={Index}></Route>
        <Route path='/dashboard/two' component={Two}></Route>
        <Route path='/dashboard/three' component={Three}></Route>
      </div>
    )
  }
}
```

![&#x5728;&#x8FD9;&#x91CC;&#x63D2;&#x5165;&#x56FE;&#x7247;&#x63CF;&#x8FF0;](https://img-blog.csdnimg.cn/20190513230651388.png)

**match**

* params: \(object\),取 Link 传递的参数
* isExact: \(boolean\), 是否 url 完全匹配
* path: \(string\),构建嵌套路由会使用到
* url: \(string\), URL的匹配部分

**location**

* 在history中也可以找到
* 包含路由信息 可判断 是否发生改变

    ![&#x5728;&#x8FD9;&#x91CC;&#x63D2;&#x5165;&#x56FE;&#x7247;&#x63CF;&#x8FF0;](https://img-blog.csdnimg.cn/20190513233912320.png)

* 保存当前路由 pathname 信息
  * 登录后跳转之登录前的页面 
* state 可以用来储存上一个路由某些状态
  * 在跳转后调用

**history**

* length: \(number\), the number of entries in the history stack
* action: \(string\), the current action \(PUSH, REPLACE or POP\)
* location: \(object\), the current location
* push\(path, \[state\]\): \(function\), pushes a new entry onto the history stack
* replace\(path, \[state\]\): \(function\), replaces the current entry on the history stack
* go\(n\): \(function\), moves the pointer in the history stack by n entries
* goBack\(\): \(function\), equivalent to go\(-1\)
* goForward\(\): \(function,\) equivalent to go\(1\)
* block\(prompt\): \(function\), prevents navigation

