## js 代码压缩
目前前端工程化中使用 [terser (opens new window)](https://terser.org/docs/api-reference#compress-options)和 [swc (opens new window)](https://swc.rs/docs/configuration/minification)进行 JS 代码压缩，他们拥有相同的 API。
1. 去除多余字符: 空格，换行及注释
2. 压缩变量名：变量名，函数名及属性名
3. 解析程序逻辑：合并声明以及布尔值简化
4. 解析程序逻辑: 编译预计算