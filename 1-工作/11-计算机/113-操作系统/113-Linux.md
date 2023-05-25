# Linux


## 杂项
### 修改环境变量 PATH
（以添加`~/bin`为例）

1. 临时修改：`PATH=~/bin:$PATH`
2. 每次登录修改
	- 一般在`$HOME`的`.bashrc`文件中添加`export PATH=~/bin:$PATH`。修改`.bashrc`后，使用`source ~/.bashrc`让其立刻生效
	- 如果使用 ssh 登陆，`.bashrc`没有用，需要写在`.bash_profile`里

### 查看文件夹大小
`du -h --max-depth=1 目录`

### 压缩和解压
tar
* 压缩：`tar [选项] [-f 压缩包名] 源文件或目录`，一般选项为 `-cvf`
* 解压：`tar [选项] 压缩包`，一般选项为 `-xvf`
* `-c`：打包
* `-x`：解压
* `-v`：显示打包文件过程
* `-f`：指定压缩包的文件名，tar 会识别其扩展名
