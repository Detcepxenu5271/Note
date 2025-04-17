# Conda


## 概述
Conda 是 Python 的包管理软件（类似 pip）

Conda 可以创建虚拟 Python 环境，可以方便地在不同环境中使用各自的 Python 版本，安装需要的库

## 基本使用
注意：Windows 需要使用 Anaconda Prompt 打开命令行
* 本质上是向命令行传入了命令
	```text
	%windir%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy ByPass -NoExit -Command "& 'E:\Environment\miniconda3\shell\condabin\conda-hook.ps1' ; conda activate 'E:\Environment\miniconda3' "
	```

env
* 查看环境：`conda env list`
* 创建环境：`conda create --name <env_name> <package_names>`
	- 如 `conda create --name OpenCV python=3.8`
* 切换环境：`conda activate <env_name>`

### 从命令行打开 Anaconda 的命令
`powershell -ExecutionPolicy ByPass -NoExit -Command "& 'E:\Environment\miniconda3\shell\condabin\conda-hook.ps1' ; conda activate 'E:\Environment\miniconda3' ; conda activate OpenCV"`
