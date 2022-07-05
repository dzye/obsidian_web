#### Map
1. 基本使用，类似对象，但是允许对象作为key
2. 构造方法，new Map(),new Map(Array),Array:[key,value]
3. 常见的属性方法
   - size
   - set
   - get
   - has
   - delete
   - clear
   - 遍历 forEach ,for...of...
4. WeakMap
   - key只能是对象
   - key的对象是弱引用，垃圾回收时不需要关心是否被WeakMap引用
   - 没有clear 不能遍历
   - Vue3 响应式原理中实际使用
