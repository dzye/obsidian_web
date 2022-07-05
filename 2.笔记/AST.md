## AST
（Abstract Syntax Tree）

### ast核心步骤
1.  Code -> AST (Parse)    //解析器(Parser)
2.  AST -> AST (Transform)    //转化器(Transformer)
3.  AST -> Code (Generate)


### 解析器
1. 词法分析
	词法分析用以将代码转化为 `Token` 流，维护一个关于 Token 的数组
	1.  代码检查，如 eslint 判断是否以分号结尾，判断是否含有分号的 token
	2.  语法高亮，如 highlight/prism 使之代码高亮
	3.  模板语法，如 ejs 等模板也离不开
2. 语法分析
	语法分析将 `Token` 流转化为结构化的 AST，方便操作