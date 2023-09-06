#### 实现原理
基础原理
hash
path 1. h5 historyApi(pushState replaceState) 2.historyApiFallback
实践方案
history 1. 兼容的平台 2. 内存路由react-router-native 3. 浏览器路由 react-router-dom
#### 工作方式
设计模式
react-router 库管理模式是  monorepo   ，使用context 上下文传递
关键模块
