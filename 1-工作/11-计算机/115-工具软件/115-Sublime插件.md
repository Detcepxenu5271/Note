# Sublime插件


## !自己写插件
[API Reference](https://www.sublimetext.com/docs/api_reference.html)

### 技巧
在 Sublime 的 Console 使用`sublime.log_command()`命令，Console 会显示命令内容（对命令进行 log）

查看官方文档（API Reference）中的 Example Plugins：`View Package File -> Default/xxx.py`

\#MARK 神奇！Sublime 的 Console 实际上是内置的 Python 解释器（交互命令行）

## Markdown Editing
### 简介
优点
1. 提供了更好的语法高亮，特点是支持的格式多，且用于格式定义的元字符被淡化，突出内容
2. 提供了便于编辑的快捷键和命令

未包含的内容
1. 没有快捷插入表格并调整格式的功能

## Vintage
### Vim入门
[VIM核心思想|ITEEDU](https://www.iteedu.com/blog/tools/vim/vimthinking)

### 不支持的操作
底行命令模式（按`:`进入）。不能进行的（有用，Sublime里没有）操作有：
1. `:n1,n2d`删除多行文本
2. `:!command`执行Linux命令，并可用`:r !command`将结果添加到文本光标处，如`:r !date`快速添加日期

`nra`：`ra`命令可将光标处的字符替换为字符a（a是任意的），而在前面加上数字n就可以将接下来的n个字符全部替换。但是在Sublime中，加上n依然只替换当前一个字符。

`R`：替换从光标开始以后的所有字符

`Ctrl+v`块状可视化模式

`Ctrl+n`或`Ctrl+p`代码提示

`m`：文本跨行移动，但Sublime里显示bookmark

`g/`和`g?`：检索命令且光标移到行首，在Sublime里不正常

`U`：撤销整行的操作

`Ctrl+r`：恢复，撤销“撤销操作”

## SFTP
### 通过密钥连接
SFTP 插件使用 Pageant 的 .ppk 密钥。如果想要通过密钥连接，除了在 SFTP 的设置文件中指定 .ppk 文件的路径，还需要在 Windows 系统上运行 PuTTY 的 Pageant 服务（添加环境变量后，可以通过命令 pageant 快速启动）

## BracketHighlighter
### 括号高亮样式
在设置文件的`user_bracket_styles`中修改。

使用自定义颜色的方式：[Example: Specifying Custom Colors in Schemes](https://facelessuser.github.io/BracketHighlighter/customize/#example-specifying-custom-colors-in-schemes)
