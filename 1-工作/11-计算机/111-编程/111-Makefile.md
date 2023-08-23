# Makefile


## 快速使用
Makefile 由一系列规则构成，规则的结构为：
> 目标文件：依赖文件
> 	命令 1
> 	命令 2
> 	...
> 	命令 n

注意：命令必须以 Tab 开头（不能用空格）

默认目标：一定是第一个目标（不管是文件还是伪目标）

伪目标
* 使用`.PHONY`指定的作用：即使存在同名文件，这个也是伪目标

## 参考资料

[GNU Make 教程（英文）](https://www.gnu.org/software/make/manual/make.html)

这个教程好：[跟我一起写 Makefile](https://seisman.github.io/how-to-write-makefile/introduction.html)
