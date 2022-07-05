## webpack 构建性能优化
1. 评估：使用 [speed-measure-webpack-plugin (opens new window)](https://github.com/stephencookdev/speed-measure-webpack-plugin)可评估每个 loader/plugin 的执行耗时
2. 更快的 loader:  [swc (opens new window)](https://swc.rs/)
	当 loader 进行编译时的 AST 操作均为 CPU 密集型任务，使用 Javascript 性能低下，此时可采用高性能语言 rust 编写的 `swc`
1. 持久化缓存: cache
2. 多进程: thread-loader
