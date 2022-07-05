## Long Term Cache
1. 使用 `webpack` 等打包器进行打包时，每个资源都可生成一个带有 hash 的路径
2. 添加 `hash` 的资源设置永久缓存，可大幅度提高该网站的缓存能力，从而大幅度提高网站的二次加载性能。
3. 当源文件内容发生变更时，资源的 `hash` 发生变化，生成新的可永久缓存的资源地址
4. 如果前端通过 docker/k8s/helm 进行部署，可由团队人员自行在构建 nginx 镜像时进行添加响应头字段。此处可作为前端性能优化的 kpi/okr。
5. 通过 `optimization.chunkIds` 可设置确定的 chunId，来增强 Long Term Cache 能力