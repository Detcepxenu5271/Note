# HTML


## Emmet
### 简介
一种用于简化 HTML、CSS、XML 输入的语法

[Cheat Sheet](https://docs.emmet.io/cheat-sheet/)

### 总结
1. 结构
	- `>`：子结构（Child）
	- `+`：同级结构（Sibling）
	- `^`：返回上一级（Climb-up）
	- `()`：分组（Grouping）
	- `*`：重复（Multiplication）
2. 计数
	- `$`：12345 计数（Item numbering）
3. 属性和内容
	- `#`：ID
	- `.`：CLASS
	- `[]`：自定义属性
		+ `p[a=1 b='value' c]`：
			```html
			<p a="1" b="value" c=""></p>
			```
	- `{}`：内容（Text）
4. HTML
	- `!`：Alias of html:5
