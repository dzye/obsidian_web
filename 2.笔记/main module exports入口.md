## main module exports入口
### main
`main` 指 npm package 的入口文件，当我们对某个 package 进行导入时，实际上导入的是 `main` 字段所指向的文件。
`main` 是 CommonJS 时代的产物，也是最古老且最常用的入口文件

### module
使用 `import` 对该库进行导入，则首次寻找 `module` 字段引入，否则引入 `main` 字段

### exports
`exports` 可以更容易地控制子目录的访问路径，也被称为 `export map`
不在 `exports` 字段中的模块，即使直接访问路径，也无法引用！
`exports` 不仅可根据模块化方案不同选择不同的入口文件，还可以根据环境变量(`NODE_ENV`)、运行环境(`nodejs`/`browser`/`electron`) 导入不同的入口文件。