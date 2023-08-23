# Windows命令行


## 重定向
### powershell文件重定向
在powershell中，输出重定向可以与cmd相同，但输入重定向不可以使用`<`。  
可以采用的一种方法为：`gc in.txt | ./program > out.txt`，其中`gc`是指令`Get-Content`的缩写。

## 使用技巧
### 输出太长，一页显示不下
在命令末尾添加`|more`，将命令输出通过管道作为命令more的输入，用于分页显示数据

### 以管理员模式运行
在终端输入如下命令（以powershell为例）：`start-process powershell -verb runas`  
将打开新窗口，保持当前配色、字体等

### 获取程序返回值
使用`%errorlevel%`变量，例如`echo %errorlevel%`
