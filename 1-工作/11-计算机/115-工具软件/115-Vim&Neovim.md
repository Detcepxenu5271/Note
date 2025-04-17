# Vim&Neovim


## 优秀教程
vimtutor
[笨方法学Vimscript（中文翻译）](https://www.kancloud.cn/kancloud/learn-vimscript-the-hard-way/49321)

## 安装和配置 Neovim
### 安装最新版本
（如果本地已经安装旧版本，可能要先卸载）

运行命令：
```bash
sudo add-apt-repository ppa:neovim-ppa/stable
sudo apt-get update
sudo apt-get install neovim
```

### 使用他人的配置
来源：[我的现代化Neovim配置 - ayamir](https://github.com/ayamir/nvimdots)
新来源：[现代Neovim配置 - 南风璇](https://zhuanlan.zhihu.com/p/532361193)

基于 lua 的配置

#### 插件方案
使用 Packer 管理插件
* 安装 Packer：`git clone --depth 1 https://github.com/wbthomason/packer.nvim ~/.local/share/nvim/site/pack/packer/start/packer.nvim`
* 首先修改相应配置文件
* 在 nvim 里输入命令`:PackerSync`安装，`:PackerClean`卸载

#### 备注
本地 wsl1 的 lazygit 未安装成功

依赖
* lldb 太大了（三百兆），没装
* nvm 没理解，不能用 apt 直接安装，没装

## 痛点解决
输入法切换问题（在插入模式下输入中文，切换到命令模式时输入法还是中文，需要手动切换，而且再次进入插入模式还要切回来）
* 使用 [im-select.exe](https://github.com/daipeihust/im-select) 命令可以切换输入法，然后在 vim 的配置中添加如下命令：
    ```text
    autocmd VimEnter * !D:\\im-select\\im-select.exe 1033
    autocmd InsertEnter * :silent :!D:\\im-select\\im-select.exe 2052
    autocmd InsertLeave * :silent :!D:\\im-select\\im-select.exe 1033
    autocmd VimLeave * !D:\\im-select\\im-select.exe 2052
    ```

## 配置 Vim
### 自定义命令
\#自定义命令 \#command

#### 参数
参数数量

在命令中使用参数 (指定参数位置)
* `<args>`
* `<q-args>` 把特殊字符转义, 例如 " -> \"
* `<f-args>` 转换为适合函数调用的格式

#### 元字符
expand
* `h expand` 可以查询

用来表示文件名
* `%` 当前文件
* `#` alternate 文件

可以加 Modifier, 如 `%:r`
* `:r` root, 去除一个扩展名

## 杂项
### 命令行参数
在打开 vim 时执行命令
* `nvim +%s/apple/banana/g 文件`：打开文件，将所有 apple 替换为 banana
    - 如果不加 %，效果是：只替换第一个 apple

### 函数式替换
注：vim 搜索替换中的正则表达式元字符需要转义，也就是说转义了才表示元字符

`:'<,'>s/#\+\s3.3.\zs\d\+\ze./\=submatch(0)+1/`
* 在 visual 模式下选中的区域，将“### 3.3.1231”格式中的数字“1231”替换为加一后的值
* `#` 重复若干次

### 删除操作的剪切问题
> 当使用p命令返回行时，您将粘贴（易失性）默认寄存器 的内容，该寄存器""已被覆盖dd。但是您仍然可以从（非易失性）yank寄存器粘贴 "0，不会被delete命令覆盖dd。

两种方案
* 按键映射，将 `x` 等映射为 `"_x`（剪切到黑洞寄存器）
* 粘贴时使用 `"0p`（从非易失寄存器粘贴）

### 时间戳
\#vim \#vim寄存器 \#vimscript
插入时间戳: `"=strftime('%c')<Ret>p`

### 按键映射
vim 的按键映射生效在不同的模式, 如下表:
```
         Mode  | Norm | Ins | Cmd | Vis | Sel | Opr | Term | Lang |
Command        +------+-----+-----+-----+-----+-----+------+------+
[nore]map      | yes  |  -  |  -  | yes | yes | yes |  -   |  -   |
n[nore]map     | yes  |  -  |  -  |  -  |  -  |  -  |  -   |  -   |
[nore]map!     |  -   | yes | yes |  -  |  -  |  -  |  -   |  -   |
i[nore]map     |  -   | yes |  -  |  -  |  -  |  -  |  -   |  -   |
c[nore]map     |  -   |  -  | yes |  -  |  -  |  -  |  -   |  -   |
v[nore]map     |  -   |  -  |  -  | yes | yes |  -  |  -   |  -   |
x[nore]map     |  -   |  -  |  -  | yes |  -  |  -  |  -   |  -   |
s[nore]map     |  -   |  -  |  -  |  -  | yes |  -  |  -   |  -   |
o[nore]map     |  -   |  -  |  -  |  -  |  -  | yes |  -   |  -   |
t[nore]map     |  -   |  -  |  -  |  -  |  -  |  -  | yes  |  -   |
l[nore]map     |  -   | yes | yes |  -  |  -  |  -  |  -   | yes  |
```

### 缓冲区 buffer
新建缓冲区的方法
* new 新建空缓冲区, 在新窗口
* enew 新建空缓冲区, 在当前窗口, 当前文件要先保存 (可以用 ! 丢弃当前文件的修改)
* edit: 编辑指定文件/新建文件

关闭窗口, 但是保留缓冲区
* close
* CTRL-W c

修改缓冲区文件名, 但不保存文件
* file <文件名>

### 显示特定行
可以用 global 命令, 匹配符合的行, 执行 `#` 命令 (print 当前行, 带行号)

这种方法可以用来显示 Markdown 大纲

示例: `:global/^#/#`

