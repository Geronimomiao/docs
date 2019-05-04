# Virtual DOM

**引子**

* 直接对DOM进行增删改操作 每一次对DOM的修改 都会引起浏览器对网页重新布局和重新渲染
* 有这么一句话: 
  * 软件开发中遇到的所有问题都可以 通过加一层抽象而得已解决
  * DOM效率低下的问题 同样可以通过加一层抽象解决

**虚拟DOM**

* 虚拟DOM使用JS对象描述DOM元素
* React 元素本身就是一个虚拟DOM节点

```text
<div className="foo">
    <h1>Hello React</h1>
</div>


{
    type: 'div',
    props: {
        className: 'foo',
        children: {
            type: 'h1',
            props: {
                children: 'Hello React'
            }
        }
    }
}
```

**Diff算法**

React 采用声明式API描述UI结构, 每次组件状态或属性更新, 组件render方法都会返回一个新的虚拟DOM对象。React会通过比较两次虚拟DOM结构的变化找出差异部分,跟新到真实DOM上，从而减少真实DOM上执行的操作。

React基于两个假设进行DOM比较

* 如果两个元素类型不同 他们将生产两颗不同的树
* 为列表中元素设置Key属性 用key标识对应元素在多次render过程中是否发生变化

**当根结点是不同类型**

p-&gt;div \|\| ComponentA-&gt;ComponentB \|\| componentA -&gt; div React会认为新的树和旧的树完全不同 不会再继续比较其他的属性和子节点 而是把整颗树拆掉\(包括虚拟DOM树和真实DOM树\)

**当根结点是相同DOM元素类型**

React 会保留根节点 比较根节点的属性 然后更新变化了的属性

**当根结点是相同组件类型**

这一过程组件实例的componentWillReceiveProps\(\) componentWillUpdate\(\)会被调用 React 无法直接知道如何更新真实的DOM树 需要在组件更新且render方法执行完成后 根据render 返回虚拟DOM结构 决定如何更新真实的DOM树

**比较完根结点 React会以同样的原则继续递归比较子节点 每一个子节点相对于其层级一下的节点来说又是一个根结点 直到比较完两颗树\(虚拟DOM\)上的所有节点 计算最终得到的差异 跟新到DOM树中**

**Key值的绑定**

* 当一个节点有多个子节点时 react 只会按照顺序逐一比较两颗树上对应子节点
* 则在列表前插入一个元素 会导致整个列表都被修改

```text
<li>first</li>
<li>second</li>


<li>third</li>
<li>first</li>
<li>second</li>
```

* 为了解决这种低效的更新方式 React提供了一个Key属性\(Key就是为了帮助React提高Diff算法效率\)
  * 每次渲染后 只要子组件的值没变 React就认为这是同一个节点

```text
<li key="first">first</li>
<li key="second">second</li>


<li key="third">third</li>
<li key="first">first</li>
<li key="second">second</li>
```

**定义key之后 React就能判断出这个节点为新增节点 其余二个节点没有发生改变 只是位置发生变化**

**这里同时揭露了一个问题，尽量不要使用元素在列表中的索引做key 因为列表中元素一旦发生改变 就可能导致大量的key失效 进而引起大量修改操作**

**如下写法应尽量避免**

```text
<ul>
    {list.map(item, index) => <li key={index}>{item}</li>}
</ul>
```

**补充**

虚拟DOM非React独有 是一个独立的技术 只不过React使用这项技术 提高自身性能



