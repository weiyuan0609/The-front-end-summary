### react和vue的区别

相同点：

- 都支持服务端渲染
- 都有Virtual DOM，组件化开发，通过props参数进行父子组件数据的传递，都实现webComponents规范
- 数据驱动视图
- 都有支持native的方案，React的React native，Vue的weex

不同点：

- React严格上只针对MVC的view层，Vue则是MVVM模式
- virtual DOM 不一样
vue会跟踪每一个组件的依赖关系，不需要重新渲染整个组件树。而对于React而言，每当应用的状态被改变时，全部子组件都会重新渲染。当然，这可以通过shouldComponentUpdate这个生命周期方法来进行控制，
- 组件写法不一样
React 推荐的做法是 JSX + inline style，也就是把 HTML 和 CSS 全都写进 JavaScript 了，即”all in js”
Vue 推荐的是使用 `webpack + vue-loader` 的单文件组件格式，即html,css,js写在同一个文件；
- 数据绑定：Vue有实现了双向数据绑定，React数据流动是单向的
- state对象在react应用中是不可变的，需要使用setState方法更新状态；在Vue中，state对象并不是必须的，数据由data属性在Vue对象中进行管理。



### react相关

#### react的优缺点

我觉得这优缺点就因人而异，见仁见智了。

优点：

- 可以通过函数式方法描述视图组件（好处：相同的输入会得到同样的渲染结果，不会有副作用；组件不会被实例化，整体渲染性能得到提升）
- 集成虚拟DOM（性能好）
- 单向数据流（好处是更容易追踪数据变化排查问题
- 一切都是component：代码更加模块化，重用代码更容易，可维护性高
- 大量拥抱 es6 新特性
- jsx

缺点：

- jsx的一个问题是，渲染函数常常包含大量逻辑，最终看着更像是程序片段，而不是视觉呈现。后期如果发生需求更改，维护起来工作量将是巨大的
- 大而全，上手有难度



#### jsx的优缺点


允许使用熟悉的语法来定义HTML元素树
JSX 让小组件更加简单、明了、直观。
更加语义化且易懂的标签
JSX 本质是对JavaScript语法的一个扩展，看起来像是某种模板语言，但其实不是。但正因为形似HTML，描述UI就更直观了，也极大地方便了开发；
在React中babel会将JSX转换为`React.createElement`函数调用，然后将JSX转换为正确的JSON对象（VDOM 也是一个“树”形的结构）
React/JSX乍看之下，觉得非常啰嗦，但使用JavaScript而不是模板语法来开发（模板语法比较有局限性），赋予了开发者许多编程能力。

### dom diff算法和虚拟DOM

React中的render方法，返回一个DOM描述，结果仅仅是轻量级的js对象。Reactjs只在调用setState的时候会更新dom，而且还是先更新Virtual Dom，然后和实际DOM比较，最后再更新实际DOM。

React.js 厉害的地方并不是说它比 DOM 快（这句话本来就是错的），而是说不管你数据怎么变化，我都可以以最小的代价来更新 DOM。方法就是我在内存里面用新的数据刷新一个虚拟的 DOM 树，然后新旧 DOM 树进行比较，找出差异，再更新到真正的 DOM 树上。

当我们修改了DOM树上一些节点对应绑定的state，React会立即将它标记为“脏状态”。在事件循环的最后才重新渲染所有的脏节点。在实际的代码中，会对新旧两棵树进行一个深度优先的遍历，这样每个节点都会有一个唯一的标记，每遍历到一个节点就把该节点和新的的树进行对比。如果有差异的话就记录到一个对象里面，最后把差异应用到真正的DOM树上。
算法实现
1 步骤一：用JS对象模拟DOM树
2 步骤二：比较两棵虚拟DOM树的差异
3 步骤三：把差异应用到真正的DOM树上
这就是所谓的 diff 算法

dom diff采用的是增量更新的方式，类似于打补丁。React 需要为数据添加 key 来保证虚拟 DOM diff 算法的效率。key属性可以帮助React定位到正确的节点进行比较，从而大幅减少DOM操作次数，提高了性能。


`virtual dom`，也就是虚拟节点。它通过JS的Object对象模拟DOM中的节点，然后再通过特定的render方法将其渲染成真实的DOM节点。
http://react-china.org/t/dom/638

- 为什么js对象模拟DOM会比js操作DOM来得快

为了解决频繁操作DOM导致Web应用效率下降的问题，React提出了“虚拟DOM”（virtual DOM）的概念。Virtual DOM是使用JavaScript对象模拟DOM的一种对象结构。DOM树中所有的信息都可以用JavaScript表述出来，例如：
```
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```
可以用以下JavaScript对象来表示：
```
{
  tag: 'ul',
  children: [{
    tag: 'li', children: ['Item 1'],
    tag: 'li', children: ['Item 2'],
    tag: 'li', children: ['Item 3']
  }]
}
```
这样可以避免直接频繁地操作DOM，只需要在js对象模拟的虚拟DOM进行比对，再将更改的部分应用到真实的DOM树上

- react组件性能优化

使用PureRenderMixin、shouldComponentUpdate来避免不必要的虚拟DOM diff，在render内部优化虚拟DOM的diff速度，以及让diff结果最小化。

#### react组件间的数据传递

1.兄弟组件不能直接相互传送数据，此时可以将数据挂载在父组件中，由两个组件共享

2.子组件向父组件通讯，可以通过父组件定义事件（回调函数），子组件调用该函数，通过实参的形式来改变父组件的数据来通信

```javascript
//子组件
this.props.onCommentSubmit({author, content, date:new Date().getTime()});
//父组件
render(){
    return(
      <div className="m-index">
        <div>
          <h1>评论</h1>
        </div>
        <CommentList data={this.state.data} />
        <CommentForm onCommentSubmit={this.handleCommentSubmit.bind(this)} />
      </div>
    )
}
```


3.非父子组件间的通信：可以使用全局事件来实现组件间的沟通，React中可以引入eventProxy模块，利用`eventProxy.trigger()`方法发布消息，`eventProxy.on()`方法监听并接收消息。

4.组件间层级太深，可以使用上下文方式，让子组件直接访问祖先的数据或函数，通过`this.context.xx`

#### 无状态组件

无状态组件其实本质上就是一个函数，传入props即可，没有state，也没有生命周期方法。组件本身对应的就是render方法。例子如下：

```javascript
function Title({color = 'red', text = '标题'}) {
  let style = {
    'color': color
  }
  return (
    <div style = {style}>{text}</div>
  )
}
```

无状态组件不会创建对象，故比较省内存。没有复杂的生命周期方法调用，故流程比较简单。没有state，也不会重复渲染。它本质上就是一个函数而已。

对于没有状态变化的组件，React建议我们使用无状态组件。总之，能用无状态组件的地方，就用无状态组件。
#### 高阶组件

高阶组件（HOC）是函数接受一个组件，返回一个新组件。其前身其实是用ES5创建组件时可用的mixin方法，但是在react版本升级过程中，使用ES6语法创建组件时，认为mixin是反模式，影响了react架构组件的封装稳定性，增加了不可控的复杂度，逐渐被HOC所替代。
实现高阶组件的方式有：

- 属性代理

```javascript
import React, { Component } from 'React';
//高阶组件定义
const HOC = (WrappedComponent) =>
  class WrapperComponent extends Component {
    render() {
      return <WrappedComponent {...this.props} />;
    }
}
//普通的组件
class WrappedComponent extends Component{
    render(){
        //....
    }
}

//高阶组件使用
export default HOC(WrappedComponent)
```
- 反向继承

反向继承是指返回的组件去继承之前的组件(这里都用WrappedComponent代指)

```javascript
const HOC = (WrappedComponent) =>
  class extends WrappedComponent {
    render() {
      return super.render();
    }
  }
```

我们可以看见返回的组件确实都继承自WrappedComponent,那么所有的调用将是反向调用的(例如:super.render())，这也就是为什么叫做反向继承。
　　
#### react事件和传统事件有什么区别吗

React 实现了一个“合成事件”层（synthetic event system），这个事件模型保证了和 W3C 标准保持一致，所以不用担心有什么诡异的用法，并且这个事件层消除了 IE 与 W3C 标准实现之间的兼容问题。

“合成事件”还提供了额外的好处：

- 事件委托

“合成事件”会以事件委托（event delegation）的方式绑定到组件最上层，并且在组件卸载（unmount）的时候自动销毁绑定的事件。



#### react组件生命周期

![](lifecycle.jpeg)

react组件更新过程：

- props/state change：

1.componentWillReceiveProps(nextProps)

只要是父组件的render被调用，在render中被渲染的子组件就会经历更新的过程。不管父组件传给子组件的props有没有改变，都会触发子组件的此函数被调用。注意：通过setState方法触发的更新不会调用此函数

2.shouldComponentUpdate(nextProps,nextState)
3.componentWillUpdate
4.render
5.componentDidUpdate