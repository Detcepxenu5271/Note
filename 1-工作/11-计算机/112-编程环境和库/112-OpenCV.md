# OpenCV


## 环境
### Python 安装
Python3.10 通过 pip 安装 OpenCV

`import cv2`, 出现报错 `ImportError: DLL load failed while importing cv2: 找不到指定的模块。` 的解决方法: 手动下载对应 Python 版本的 whl 包 (可以从 [清华源](https://pypi.tuna.tsinghua.edu.cn/simple/opencv-python/) 下载), 使用 `pip install 文件名` 安装

### Windows 下 MinGW 编译 OpenCV 源代码
为什么要手动编译？
> Q: 想问下为什么在windows环境下不使用官方预编译好的opencv
> A: 因为官方的是MVC编译的，GCC下用不了。我更喜欢GCC编译器，GCC更加灵活。

### C++ 命令行编译
#### Windows 平台编译
参考教程1：[](https://zhuanlan.zhihu.com/p/402378383)
* MinGW 编译遇到问题：[opencv通过mingw编译出现的问题](https://blog.csdn.net/weixin_50988214/article/details/115100251)
* 编译单文件命令：
```shell
g++ hello_opencv.cpp -o hello_opencv.exe
	-std=c++11 \
    -I E:\\Environment\\opencv\\install\\include \
    -L E:\\Environment\\opencv\\install\\x64\\mingw\\lib \
    -lopencv_core460 -lopencv_imgcodecs460 -lopencv_imgproc460 -lopencv_calib3d460 -lopencv_dnn460 -lopencv_features2d460 -lopencv_flann460 -lopencv_gapi460 -lopencv_highgui460 -lopencv_ml460 -lopencv_objdetect460 -lopencv_photo460 -lopencv_stitching460 -lopencv_video460 -lopencv_videoio460 \
```
`g++ hello_opencv.cpp -o hello_opencv.exe -std=c++11 -I E:\\Environment\\opencv\\install\\include -L E:\\Environment\\opencv\\install\\x64\\mingw\\lib -lopencv_core460 -lopencv_imgcodecs460 -lopencv_imgproc460 -lopencv_calib3d460 -lopencv_dnn460 -lopencv_features2d460 -lopencv_flann460 -lopencv_gapi460 -lopencv_highgui460 -lopencv_ml460 -lopencv_objdetect460 -lopencv_photo460 -lopencv_stitching460 -lopencv_video460 -lopencv_videoio460`
* 注意：这个杀千刀的`hello_opencv.cpp -o hello_opencv.exe`要放在前面，否则会出现 undefined 错误 \#Check
* 没有找到 float.h 的错误
	- clang 编译包含了 float.h 头文件的 cpp 文件时，会有 `'float.h' file not found` 的报错
	- 尝试了更换新的 float.h 文件（LLVM 中），无效
	- 根据报错信息和 `clang -v` 得出的编译信息，追踪到错误原因：`../mingw64/x86_64-w64-mingw32/include` 中 float.h 的第 28 行的 `#include_next<float.h>` 应该去找 `../mingw64/lib/gcc/x86_64-w64-mingw32/8.1.0/include` 下的 float.h 文件（实际上 g++ 可以找到），但是 clang 接下来只包含了 `mingw64/lib/gcc/x86_64-w64-mingw32/8.1.0/include/c++` 目录，所以 #include_next 找不到 float.h 文件了
	- 最终解决方法：`New-Item -ItemType SymbolicLink -Path "D:/2-Code/0-basic/MinGW64/lib/gcc/x86_64-w64-mingw32/8.1.0/include/c++/float.h" -Target "D:/2-Code/0-basic/MinGW64/lib/gcc/x86_64-w64-mingw32/8.1.0/include/float.h"`（在 clang 包含的 `../mingw64/lib/gcc/x86_64-w64-mingw32/8.1.0/include/c++` 路径中，添加一个软链接，链接到 `../mingw64/lib/gcc/x86_64-w64-mingw32/8.1.0/include` 的 float.h 中）

#### Linux 平台编译
参考教程2：[Ubuntu 安装 OpenCV（亲测有效）](https://blog.csdn.net/weixin_44785513/article/details/113825117)
参考教程3：[在 Ubuntu 20.04 上安装 OpenCV](https://blog.csdn.net/qq_58060770/article/details/127553911)

CMake 命令
```bash
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
```

Make 命令：`make -j2`

安装命令：`make install`

配置环境：
* 参照“参考教程2”
* 手动添加`/usr/local/lib/pkgconfig/opencv.pc`文件，内容为：
	```text
	prefix=/usr/local
	exec_prefix=${prefix}
	includedir=${prefix}/include
	libdir=${exec_prefix}/lib
	
	Name: opencv
	Description: The opencv library
	Version:4.6.0
	Cflags: -I${includedir}/opencv4
	Libs: -L${libdir} -lopencv_shape -lopencv_stitching -lopencv_objdetect -lopencv_superres -lopencv_videostab -lopencv_calib3d -lopencv_features2d -lopencv_highgui -lopencv_videoio -lopencv_imgcodecs -lopencv_video -lopencv_photo -lopencv_ml -lopencv_imgproc -lopencv_flann  -lopencv_core
	```
	（参考 [Package opencv was not found in the pkg-config search path.](https://blog.csdn.net/PecoHe/article/details/97476135)）

## 教程
### 4h上手C++版Opencv（搬运）
B 站视频（搬运）：[4h上手C++版Opencv](https://www.bilibili.com/video/BV11A411T7rL/?spm_id_from=333.337.search-card.all.click&vd_source=2c135662f2e5e0a38199900dd4a72b3b)
CSDN 笔记：[【OpenCV（C++）快速入门】--上篇--计算机图像颜色基础理论](https://blog.csdn.net/weixin_45703465/article/details/122583084?utm_source=app&app_version=5.0.0)

#### 1
灰度图像
* 一个像素由 1 byte（256）表示

### 计算机视觉入门到精通！公认讲的最好的【OpenCV计算机视觉教程】同济大佬12小时...
#### P4 计算机眼中的图像

