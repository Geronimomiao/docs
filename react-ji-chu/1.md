# react 起步一



**开发环境**

* npm i -g create-react-app
* create-react-app \[app name\]

**JSX 基础语法**

* JS 里直接写 html
* class 要写成 className
* 变量用 {} 包裹

**小知识点**

* 一个组件只能返回一个根结点
* class 类名 大写
* 一类只有 render\(\){} 可以用函数代替 \(以下两种写法等价\)

```text
function Cavalry(props) {
  return <h2>骑兵连连长 {props.boss}</h2>
}


class Cavalry extends React.Component{
  render() {
    return <h2>骑兵连连长 {this.props.boss}</h2>
  }
}
```

