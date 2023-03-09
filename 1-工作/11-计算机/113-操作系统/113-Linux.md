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
