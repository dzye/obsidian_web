## Tree Shaking
1. 基于 ES Module 进行静态分析，通过 AST 将用不到的函数进行移除，从而减小打包体积。
2. `import *`， JSON 格式都可以生效