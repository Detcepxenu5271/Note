# Note——以纯文本为主的个人笔记库


## 一、概述
## 二、笔记结构（第一版）
### 命名规范
#### 文件夹
所有文件夹以“编号+下划线”的格式开头：
1. 一级目录的编号为0-9。
2. 二级目录为10，11，……，19，20，21，……一直到99。第一个数字对应所在的一级目录，第二个数字表明具体类别。
3. 三级目录以此类推，为100-999。
4. 二、三级目录不以0开头的原因是：一级目录Inbox没有子目录。

#### 文件
除了Inbox文件和一、二级目录的索引文件外，所有的文件以所在三级目录的编号+下划线开头，后缀名为.md，中间则是该条目的具体名称。

#### 通用
1. 以杜威十进制分类法对三级目录命名。
2. 如需要用空格，用下划线代替。

### 文件结构
所有的文件以相对目录方式的前提处理，这意味着将Note文件夹迁移到任何位置，笔记的所有资源都是完整一致的。

所有Markdown中引用的图片都存储在Img目录下，按`日期_时间[_说明]`的格式命名（说明可以省略）。例如：`2022-03-31_09-58-26_测试图片`

## 三、工具说明
### 3.1 文本编辑器
Sublime Text 4
* 关键插件
	1. Markdown Editing

Visual Studio Code
* 关键插件
    1. Markdown All in One

备注
1. 无序列表
    - 在使用 Sublime 的 Markdown Editing 插件时，无序列表使用“*，-，+”循环的方式，也就是一级列表用`*`，二级用`-`，以此类推
    - 在使用 VSCode 的 Markdown All in One 插件时，无序列表只用`-`

### 3.2 内容查看与导出
Typora (with Pandoc)

### 3.3 云端保存与同步
Gitee
* 项目地址：[Note][https://gitee.com/detcepxenu5271/note]

## 四、使用方法
