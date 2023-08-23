# The Binding of Isaac


## Mod 制作
[API 文档](https://wofsauge.github.io/IsaacDocs/rep/index.html)

### Lua 基础
（一些可以注意的地方）

运算符
* `~=`：表示不等于
* `^` 表示乘方

独特的运算符
* `..`：字符串连接，可以将非字符串转化为字符串
* `#`：取长度

逻辑判断只有 false 和 nil 为假

赋值可以用逗号，例如 `a, b, c = 1, 2, 3`

条件判断
* ```lua
	if ... then
		...
	elseif ... then
		...
	else
		...
	end
	```

三种循环
1. ```lua
	while (...) do
		...
	end
	```
2. ```lua
	for i = 1, 10, step do
		...
	end
	```
	- **注意 for 中的表达式只会在一开始算一次！**
3. ```lua
	repeat
		...
	until (...)
	```

循环：有 break 没有 continue

函数定义的两种方法
1. ```lua
	MyFunction =
	function (x, y)
		-- body
	end
	```
2. ```lua
	function MyFunction(x, y)
		-- body
	end
	```

函数参数传递：少穿则赋 nil，多传忽略

表（table）
* lua 的表就是 python 的字典
* 定义的 key 要用 `[]` 括起来，除非是字符串（可以同时省略 `[]` 和 `""`）
* 访问时，如果 key 是字符串，可以用 `.` 访问
* 表可以当对象用

**lua 的下标从 1 开始！**
