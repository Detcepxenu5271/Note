# CMake


## 杂项
### 指定编译工具
按步骤编译cmake时出现错误：
```text
-- Building for: NMake Makefiles
-- The C compiler identification is unknown
-- The CXX compiler identification is unknown
```
（之后就出现了错误）

问题是Build方式不对，默认使用NMake，但NMake是VS的，我没有安装VS

一种解决
* 将MinGW的目录mingw64\bin下的mingw32-make.exe复制一份，重命名为make.exe
* 步骤c换成cmake -G"Unix Makefiles" ../

进阶：Generator（生成器）
* 用于适配不同种类的项目开发环境
* 举例：Visual Studio 10，NMake Makefiles，MinGW Makefiles，Unix Makefiles，CodeBlocks - MinGW Makefiles等等
* 我采用的方法（随后步骤和教程相同）
  1. 在CMake（gui）里选择File-Delete Cache
  2. 点击Configure将默认generator改为MinGW Makefiles

再进阶
* 默认Generator在每个项目的Cache文件里。例如第一次使用-G指定生成器，以后直接用cmake ..就是之前所用的生成器
