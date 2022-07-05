#### Symbol
1. 基本使用
   - 作为唯一性的对象属性名使用，防止重置掉对象本身的属性
   - Symbol('xxx') 创建的时候可以传入一个描述
   - 不能通过xxx.xxx获取Symbol为key的属性值
   - 遍历/Object.keys()/getOwnPropertyNames()无法获取Symbol为key的属性，只能通过Object.getOwnPropertySymbols()获取
   - Symbol.for(描述),创建相等的Symbol（todo）