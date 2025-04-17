# Linux


## 命令行
### 重定向
命令 `command >/dev/null 2>&1` 解释
* stdin, stdout, stderr 的文件描述符默认为 0, 1, 2
* `>` 表示输出重定向, 默认文件描述符为 1, 可以指定
* `/dev/null` 表示黑洞文件, 输入将被丢弃
* `2>&1` 表示将错误输出重定向到标准输出
	- 其中, `&1` 表示用文件描述符指定文件, 而非文件名
	- 不将错误直接重定向到 `/dev/null` 是因为多个输出重定向到同一个文件会导致错乱

### 执行多条命令
三种方法
* `command1 ; command2 ...` 用 ; 分隔, 不管前一条命令是否执行成功, 都会执行下一条
* `command1 && command2 ...` 用 && 分隔, 只有前一条命令执行成功, 才会执行下一条
* `command1 || command2 ...` 用 || 分隔, 只有前一条命令执行失败, 才会执行下一条

## 常用命令
### 文件操作
#### 移动、复制、重命名
`rename`
* 示例: `rename 's/a_/b_/' *.c`
	* 对 (当前目录下) 所有 .c 文件, 将文件名中的 a_ 替换为 b_

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

### 文件同步
rsync
* [阮一峰的教程](https://www.ruanyifeng.com/blog/2020/08/rsync.html)
* 基本使用: `rsync [OPTIONS] SRC DES`
* 参数
	- `-a`: 递归同步，且同步元信息
	- `-n`: 模拟执行结果
	- `--delete`: 删除目标目录有，但源目录没有的文件，保证同步过去的文件相同
	- `-v`: 显示过程
	- `-h`: 友好显示
	- `-u`: update，不覆盖同名且更新的文件（默认覆盖）
* 示例
	- `rsync -avh src/ ubuntu@xxx.xxx.xxx.xxx:/home/ubuntu/des`
		将 src 目录下的所有文件同步到远程服务器的 /home/ubuntu/des 目录下（没有会创建）
