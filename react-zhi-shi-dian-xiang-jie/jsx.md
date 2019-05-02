# JSX

**JSX 简介**

JSX 是用来描述UI的 JS 扩展语法 长期以来 UI 和 数据分离 一直是前端一个重要关注点 React 致力于通过组件概念将页面拆分 并实现组件复用 React 认为 一个组件应该是 具备UI描述 和UI数据的完整体，不应该分开处理，于是发明 JSX 作为UI描述和UI数据之间的桥梁

**标签类型**

* DOM类型标签\(首字母小写\)
* 组件类型标签\(首字母大写\)

**React 通过首字母大小写判断渲染标签类型**

**JS表达式**

```text
// 给标签属性赋值
const element = <MyComponent foo={ 1 + 2 } />

// 定义子组件
const todos = ['item1', 'item2', 'item3']
const element = (
    <ul>
        {todos.map(message => <Item key={message} message={message} />)}
    </ul>
)
```

**只能是js表达式 不能是多行js语句** **可以用三目运算符代替if**

* Dom 标签
  * class 写成 className 
  * onclick 写成 onClick
* JSX 标签是React组件时 可以自定义标签或属性名 
  * &lt;User name='React' age='4' address='America'&gt;

**注释**

{/\*    \*/}

**补充**

JSX 语法只是 React.createElement\(component, props, ...children\)语法糖 所以 JSX 均会转化成对这个方法的调用

```text
const element = <div className='foo'>Hello, React</div>

const element = React.createElement('div', {className: 'foo'}, 'Hello, React')
```

