#### 共同点
使用方式：函数签名相同 
运用效果：都是用于处理副作用

#### 不同点
使用场景：
effect: 大部分场景
layoutEffect: 处理dom调整样式，避免页面闪烁
独有能力：
effect: 异步处理副作用
layoutEffect: 同步处理副作用 阻塞页面更新 
设计原理：
effect: 异步调用
layoutEffect: 同步调用 需要避免阻塞
未来趋势：