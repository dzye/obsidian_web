## 运行时Chunk加载分析

### code spliting
[Code Splitting](https://link.zhihu.com/?target=https%3A//webpack.js.org/guides/code-splitting/)其实就是把代码分成很多很多块（ **_chunk_** ）
在 webpack 中，通过 `import()` 可实现 code spliting

### 运行时解析
1. `import()` 加载数据 ，内部代码被重新编译成一个单独的文件
2. `import` 使用时，调用方法加载该文件
3. 加载文件使用了JSONP的方式引入，内部代码执行结束（猜的-todo验证）,进行删除