
#### 更新时机
react:

#### 遍历算法
react: 深度优先遍历

#### 优化策略
react: 分而治之优化，a. 树比对：同级比较 b. 组件比对 如果class一致则认为是相似的树结构，否则为不同的树结构 c. 元素比对 同级子节点 标记 key进行列表比对



react diff核心: 两次遍历，因为开发者认为页面更新时，同层级节点顺序基本不会发生变化，所以进行第一次遍历，直接遍历顺序对比列表的元素key，遍历到不可复用即停止第一次遍历，第二次遍历即遍历新vdom,去老fiber生成的map中查找，找到就移动到新的位置，剩余老的删掉，新的新增


[深入理解 React 和 Vue 的 diff 原理](https://juejin.cn/post/7255855818594254906?searchId=20230831012940F57DCE4C502637ADDEB5)
[为什么 React 的 Diff 算法不采用 Vue 的双端对比算法？](https://juejin.cn/post/7116141318853623839?searchId=2023083111553569C0AD910A8E44EAD11D)
[图解 React 的 diff 算法：核心就两个字 —— 复用](https://juejin.cn/post/7131741751152214030?searchId=2023083111553569C0AD910A8E44EAD11D)
