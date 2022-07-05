## js 资源注入 html
通过plugin实现，webpack内为 [html-webpak-plugin](https://github.com/jantimon/html-webpack-plugin)，在 rollup 的世界里，它是 [@rollup/plugin-html](https://github.com/rollup/plugins/tree/master/packages/html)
注入的原理为当打包器已生成 entryPoint 文件资源后，获得其文件名及 `publicPath`，并将其注入到 html 中