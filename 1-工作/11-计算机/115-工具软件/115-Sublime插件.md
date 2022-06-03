# Sublime插件


## Markdown Editing
### 一、简介
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
