# Python


## 面向对象
### 类中的变量
* 类属性或类变量
    - 类体中、所有函数之外定义的变量
    - 类似 C++ 的静态变量
* 实例属性或实例变量
    - 类体中，所有函数内部，以 `self.变量名` 的方式定义的变量
    - 类似 C++ 的成员变量
* 局部变量
    - 类体中，所有函数内部，以 `变量名=变量值` 的方式定义的变量
    - 类似 C++ 的局部变量

## I/O
### 格式化
格式化有三种方法：%，format 和 f-string

#### f-string
基本使用：花括号里的内容为替换字段，内容同正常的 Python 语法（而非字符串），可以使用各种值、变量、表达式、函数等。如：
```python
>>> f"They have {2+5*2} apples"
'They have 12 apples'

>>> name = "July"
>>> f"my name is {name.lower()}"
'my name is July'

>>> import math
>>> f"Π的值为{math.pi}"
'Π的值为3.141592653589793'
```

填充和截断：在大括号中间使用`:`，后面的部分指定填充长度和填充位置（也可以指定其他格式）。填充的数字后可以跟`.`和另一个数字，表示截断的长度（截断只针对字符串）。
```python
# 注：不指定填充字符，默认空格
>>> name = "Huang Wei"
>>> f"{name:_>20}" # 左填充
'___________Huang Wei'

>>> f"{name:_<20}" # 右填充
'Huang Wei___________'

>>> f"{name:_^20}" # 居中填充
'_____Huang Wei______'

>>> a = 123.456 # 浮点数
>>> f"{a:09.2f}" # 会做四舍五入
000123.46
```

## 库
### pyqt5
GUI 库，开发桌面程序

[中文教程](https://maicss.gitbook.io/pyqt-chinese-tutoral/)

#### 介绍
#### Hello World
三个步骤
* `app = QApplication(sys.argv)`，创建应用
* 创建基本窗口对象（QWidget，QMainWindow），然后进行相关设置和后续操作
* `sys.exec(app.exec_())`，退出应用

`xxx.triggered.connect(函数)`
* xxx 是 QAction 实例
* 触发 xxx 时，会调用传入的函数，可以自定义
* 除了 triggered 还有其他的行为，例如 clicked

#### 菜单和工具栏
菜单
* menubar：菜单的条，第一次调用创建新的对象，之后只返回已有的
    - menubar 通过 `xxx.menubar()` 调用，xxx 是 QWidget，QMainWindow 等类型的对象
* menu：菜单项，能展开，可以嵌套
* action：菜单中的具体选项，执行某个操作

### matplotlib
2D 绘图库，数据可视化

## Jupyter Notebook
### 杂项
#### 为什么导入自己写的模块，函数运行不正确？
当更改自己的模块的内容后，要 Restart 内核，才能反映到使用该模块的 .ipynb 文件中

## 配置环境
### Anaconda + cuda + pytorch
[一个非常好的教程](https://blog.csdn.net/qq_46126258/article/details/112698284)

首先, 从官网下载并安装 Anaconda
* ?? 建议选 Just me, 不确定 All users 会不会出问题
* 通过 `conda -V` 检查安装是否成功

然后, 从官网下载正确版本的 cuda 和 cudnn
* !! 版本首先看电脑的 nvidia 能支持的版本, 可以安装更低的版本 (也不要太低)
    其次看需要安装的 pytorch 支持的版本, 例如我使用 torch 2.0.0, 支持 cu118 (11.8)
* 通过 `nvcc -V` 检查安装是否成功

cuda 直接安装在默认路径, cudnn 文件夹放到 cuda 目录中

在安装 pytorch 前, 创建其对应的 conda 虚拟环境
* 注意 python 版本需要对应, 例如 torch 2.0.0 支持的版本在 3.8 - 3.11 之间

在 conda 环境中安装 torch, torchvision 和 torchaudio
* Pytorch 官网可以找到安装命令
* 官网的源和国内镜像不一定行, 可以在 [Pytorch下载](https://download.pytorch.org/whl/torch/) 等网站手动找到对应版本的 wheel 文件, 然后用 `pip install <wheel文件>` 命令手动安装

最后, 在 conda 环境中检查安装是否成功
* `python`
* `print(torch.__version__)`
* `torch.cuda.is_available()`