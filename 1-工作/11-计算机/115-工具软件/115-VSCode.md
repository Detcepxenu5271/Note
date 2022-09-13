# VSCode


## 杂项
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
