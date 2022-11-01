# Python


## I/O
### 格式化
格式化有三种方法：%，format 和 f-string

#### f-string
基本使用：花括号里的内容为替换字段，内容同正常的 Python 语法（而非字符串），可以使用各种值、变量、表达式、函数等。如：
```python
>>> f"They have {2+5*2} apples"
'They have 12 apples'

>>> name = "July"
>>> f"my name is {name.lower()}"
'my name is July'

>>> import math
>>> f"Π的值为{math.pi}"
'Π的值为3.141592653589793'
```

填充和截断：在大括号中间使用`:`，后面的部分指定填充长度和填充位置（也可以指定其他格式）。填充的数字后可以跟`.`和另一个数字，表示截断的长度（截断只针对字符串）。
```python
# 注：不指定填充字符，默认空格
>>> name = "Huang Wei"
>>> f"{name:_>20}" # 左填充
'___________Huang Wei'

>>> f"{name:_<20}" # 右填充
'Huang Wei___________'

>>> f"{name:_^20}" # 居中填充
'_____Huang Wei______'

>>> a = 123.456 # 浮点数
>>> f"{a:09.2f}" # 会做四舍五入
000123.46
```

## 库
### pyqt5
GUI 库，开发桌面程序

[中文教程](https://maicss.gitbook.io/pyqt-chinese-tutoral/)

### matplotlib
2D 绘图库，数据可视化
