# Create a Game Loop using C and SDL
\#Course \#C \#SDL \#GameDev

[Create a Game Loop using C and SDL](https://www.udemy.com/course/game-loop-c-sdl/)

## Overview
知识点
* Game Loop
* SDL

## Section 1: Introduction
### 1. Motivations and Learning Outcomes
```lua
SETUP()

while (true) do
	PROCESS_INPUT()
	UPDATE()
	DRAW()
end
```

### 2. Game Engines
## Section 2: Installation and Dependencies
#### 3. Project Dependencies
#### 4. Environment Setup
#### 5. Installing GCC and SDL on Linux
#### 6. Installing GCC and SDL on macOS
#### 7. Installing Visual Studio and SDL on Windows
#### 8. Choosing a Code Editor for Linux
#### Quiz 1: Quiz 1
### Section 3: Building Our Project
#### 9. Compiling Our Code with GCC
#### 10. Creating a Makefile
### Section 4: Creating a Window
#### 11. Creating an SDL Window
这一步完成，SDL 窗口还不能正常运行

### Section 5: Processing Input
#### 12. Polling SDL Events
### Section 6: Rendering
#### 13. SDL Rendering
#### 14. Drawing a Rectangle
#### Quiz 2: Quiz II
### Section 7: Updating Our Game Objects
#### 15. The Update Function
#### 16. Fixing Our Time Step
Most important part

#### 17. Updating as a Function of Delta Time
游戏内涉及到时间的变化（如物体的位移）需要乘上 delta time

#### 18. Using a Delay Function
不应该用 while 循环来延时，等到一帧的时间占满，因为 CPU 会一直执行这段代码并消耗资源，并且程序会锁在这里，而这不是必须的

SDL_Delay 使用了操作系统级的命令来实现延时

#### Quiz 3: Quiz III
### Section 8: Proposed Activity
#### 19. Proposed Activity
#### 20. Proposed Activity (Solution)
我第一次的实现：按左键把速度减一个值，最多减一次；左键抬起，把相应速度加回去。其他同理。

参考答案的实现：使用赋值，按下就赋速度，抬起赋零。

我优化后，发现效果最好的方式为：设置“is down”变量，把按键状态和速度变化分开。这样可以解决两个键同时按下时行为奇怪的问题，以及变向延迟的问题。

![](../../../img/GIF_2023-1-14_13-50-12.gif)

### Section 9: Bonus Lecture
#### 21. Conclusion & Other References
#### 22. Course Links
