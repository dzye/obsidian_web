是 还是存在三种情况 
1. 可能是a
2. 可能是b
3. ab都有可能

react17 存在当前情况    react18 全部为异步


#### 合成事件

  合成事件出现之前进行事件委托的方式绑定事件
  合成事件同事件委托，React17之前将React给document挂上事件监听，事件冒泡到document造出一个合成事件，并按组件树模拟事件冒泡；React17之后统一冒泡到dom容器（reactDom.render()调用的节点）上

  React源码中对合成事件进行罗列，列表中的才是合成事件
#### 同步场景

 addEventListener\setTimeout\setInterval这些原生事件中会同步更新，因为这些不是React封装的合成事件，没有对事件触发的setState渲染过程中executionContext进行赋值，导致一直是false, 无法进行批处理，一直是同步操作
#### 异步场景

 除去同步场景，都为异步，原因为生命周期事件，合成事件为React可控制的  ，进行过处理