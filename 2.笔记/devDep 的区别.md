## dependencies 与 devDependencies 有何区别
1. 对于业务代码而讲，它俩区别不大
2. 对于库 (Package) 开发而言，是有严格区分的
	-   dependencies: 在生产环境中使用
	-   devDependencies: 在开发环境中使用，如 webpack/babel/eslint 等
3. 当在项目中安装一个依赖的 Package 时，该依赖的 `dependencies` 也会安装到项目中，即被下载到 `node_modules` 目录中。但是 `devDependencies` 不会