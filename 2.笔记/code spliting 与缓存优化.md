## code spliting 与缓存优化

### 为什么需要分包？
1.  一行代码将导致整个 `bundle.js` 的缓存失效
2.  一个页面仅仅需要 `bundle.js` 中 1/N 的代码，剩下代码属于其它页面，完全没有必要加载

### 如何更好的分包
1. 打包工具运行时
	webpack(或其他构建工具) 运行时代码不容易变更，需要单独抽离出来，比如 `webpack.runtime.js`。由于其体积小，**必要时可注入 `index.html` 中**，减少 HTTP 请求数，优化关键请求路径
2. 前端框架运行时
	React(Vue) 运行时代码不容易变更，且每个组件都会依赖它，可单独抽离出来 `framework.runtime.js`。请且注意，**务必将 React 及其所有依赖(react-dom/object-assign)共同抽离出来**，否则有可能造成性能损耗
3. 高频库
	一个模块被 N(2 个以上) 个 Chunk 引用，可称为公共模块，可把公共模块给抽离出来，形成 `vendor.js`

### 使用 webpack 分包
在 webpack 中可以使用 [SplitChunksPlugin (opens new window)](https://webpack.js.org/plugins/split-chunks-plugin)进行分包，它需要满足三个条件:
1.  minChunks: 一个模块是否最少被 minChunks 个 chunk 所引用
2.  maxInitialRequests/maxAsyncRequests: 最多只能有 maxInitialRequests/maxAsyncRequests 个 chunk 需要同时加载 (如一个 Chunk 依赖 VendorChunk 才可正常工作，此时同时加载 chunk 数为 2)
3.  minSize/maxSize: chunk 的体积必须介于 (minSize, maxSize) 之间