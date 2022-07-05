## 非javascript资源加载

### JSON与图片
模块加载器(`loader`)将它们转化为模块的形式

### style解析
1. css-loader 处理css中的url和@import，当作模块的引入，原理就是 postcss，借用 `postcss-value-parser` 解析 CSS 为 AST，并将 CSS 中的 `url()` 与 `@import` 解析为模块
2. style-loader 将样式注入DOM，原理为使用 DOM API 手动构建 `style` 标签，并将 CSS 内容注入到 `style` 中