# VSCode


## 设置（Settings）
Windows 默认字体设置：`Consolas, 'Courier New,' monospace`

## 工作区（Workspace）
### 工作区的插件
单独为工作区设置插件的禁用和启用
* 该信息存储的位置在 local storage cache 中
    [Ability to enable extensions only on specific workspaces #15611](https:/https://github.com/microsoft/vscode/issues/15611/)
    ![存储位置](../../../img/2023-04-01-23-09-01.png)

## 调试
### 查看数组变量
方法一
`*(int(*)[10])arr_name`

方法二
`*arr_name@10`

## 插件（Extension）
### Markdown 相关
好文章：[第 6 期、写作：基于 VS Code 的 Markdown 写作技术栈](https://blog.orangex4.cool/post/lesson-zero-6/)

[](https://www.cnblogs.com/YunyaSir/p/15523927.html)

### VScode Neovim
建议少用 VScode 里的命令模式（可能会出现卡死的 BUG）

### Vim
#### 有用的命令
hover: gh

#### Bug
在使用 Profile 功能时, 有时会出现 vim 插件的 key-bindings 失效 (如 jk), Reload Window 可以解决

## 杂项
### 字体
backup：`"editor.fontFamily": "Consolas, 'Courier New', monospace"`

### Portable Mode
[官方文档](https://code.visualstudio.com/docs/editor/portable)

Windows / Linux 版
* 需要下载 .zip/.tar.gz 版本
* 需要手动建立 data 文件夹
* 更新需要手动替换 data 文件夹
* 也可以手动建立 tmp 文件夹，存放临时文件（一般默认在系统盘）

### 快捷键
| 键位             | 功能                      | 描述                             | Sublime                            |
| ---------------- | ------------------------- | -------------------------------- | ---------------------------------- |
| `Ctrl+K, Ctrl+B` | Set Selection Anchor      | 类似 Sublime 里的 Set Mark       | 切换侧边栏                         |
| `Ctrl+E`         | 同`Ctrl+P`                |                                  | 将选中文本放入搜索缓冲区           |
| `Ctrl+R`         | Open Recent               |                                  | Goto Symbol [`Ctrl+Shift+O`]       |
| `Ctrl+;`         |                           | 类似`Ctrl+K`的组合键             | Goto 无语义的 Symbol               |
| `Alt+LeftArrow`  | Go Back                   | 类似 Sublime 里的`Alt+-`         | 向左移动光标，被大写字母和符号切分 |
| 无               | Cursor Word Start Left    | 类似 Sublime 里的`Alt+LeftArrow` |                                    |
| `Alt+UpArrow`    | Move Line Up              | 行上移                           | 无                                 |
| `Ctrl+Shift+\`   | Go to Bracket             | 类似 Sublime 里的`Ctrl+M`        | 无                                 |
| `Ctrl+T`         | Go to Symbol in Workspace | 类似 Sublime 里的`Ctrl+;`        | 交换字符                           |

补充
* Anchor 的用法
    - `Ctrl+K, Ctrl+B` 设置锚点
    - `Ctrl+K, Ctrl+K` 选择到锚点（自动取消）
    - `Esc` 取消锚点
* Split View（Editor）：建议鼠标

### 配置
`files.exclude`：使用的是“glob patterns”在配置里的模式，路径以工作区的根目录为当前路径。例如 `backup` 只匹配根目录下的同名文件/文件夹。而在 search view 中，glob patterns 默认带有 `**/` 前缀，即匹配所有同名文件/文件夹
