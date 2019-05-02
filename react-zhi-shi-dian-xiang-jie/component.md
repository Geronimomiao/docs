# Component

**定义**

* 使用 ES6 类组件
  * class 继承 React.Component
  * class 内部必须定义 render 方法 render 方法返回代表该组件UI的React元素
* 使用 函数组件
  * 函数接受 props 作为参数
  * 返回代表这个组件UI的React元素结构

**分类**

* 有状态组件
  * 组件内部状态会发生改变 \(通过 state 反应\)
* 无状态组件
  * 组件内部状态不发生改变 \(即不用 state\)  
* 组件应用设计思路
  * 通过定义少数有状态组件 管理整个应用的状态变化
  * 将状态通过 props 传递给其余 无状态组件
  * 由无状态组件完成绝大部分 UI 渲染工作

**props**

* 将父组件的数据或方法传递给子组件

```text
<User name='React' age='4' address='America'>

// 此时User组件props结构如下：
props = {
    name='React',
    age='4',
    address='America'
}
```

_在接收props的组件写校验_

* 属性校验

```text
import PropTypes from 'prop-types';

class PostItem extends React.Component {
    //...
}

PostItem.propTypes = {
    post: PropTypes.object,
    onVote: PropTypes.func
}

PostItem.propTypes = {
    post: PropTypes.shape({
        id: PropTypes.number,
        title: PropTypes.string
    }).isRequired,
    onVote: PropTypes.func.isRequired
}
```

* 默认属性

```text
function Welcome(props) {
    return <h1 className='foo'>Hello, {props.name}</h1>
}

Welcome.defaultProps = {
    name: 'Stranger'
}
```

**state**

* state 是组件的内部状态 
* state 变化最终将反映到组件UI变化上
* 在组件构造方法 constructor 通过 this.state 定义组件的初状态 
* 在组件中 this.setState 改变组件的状态



**为组件添加样式**

* 外部样式    
  * 在使用组件html页面 通过标签引入
    * * 一般作用于整个应用所有组件\(基础样式表\)
  * 把样式表文件当作一个模块
    * import './style.css';
* 内联样式
  * 属性名使用驼峰格式 命名



**元素和组件**

* React 元素是一个普通的 javascript 对象 这个对象通过 Dom 节点 或 React 组件 描述界面是什么样子
* JSX 语法就是用来创建 React 元素的
* React 组件是一个 class 或函数 接收一些属性作为输入 返回一个 React 元素
* React 组件是由若干个 React 元素组建而成

**补充**

**使用ReactDOM.render\(\) 需要先导入react-dom库 这个库会完成组件所代表的虚拟DOM节点到浏览器DOM节点的转换**

**事实上 React可以看作一个函数 输入props state 输出是组件的UI**

```text
UI=Component(props, state)
```
