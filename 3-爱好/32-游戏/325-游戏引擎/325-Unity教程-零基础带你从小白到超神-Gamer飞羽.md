# 零基础带你从小白到超神 by Gamer飞羽


## 教程内容
### 如何正确学习Unity游戏开发（in 喜马拉雅）
一定要练，学差不多就要做项目

### 01. 游戏引擎是啥玩意
教程不包含 C#，需要学到什么程度：基础语法，理解面向对象，委托

游戏引擎：编写好的可重复利用的代码，以及功能编辑器

### 02 - 09

使用 2 by 3 的 Layout

在 Project 里右键，同菜单的 Assets

GameObject 具有 Component

Plane 和 Quad 的区别
* 在 Scene 右侧第一个选项（球形，Draw Mode）选择 Wireframe，发现网格不一样
* 注意，两者是单面的

【自己补充】按住右键时，滚轮调整的是 wasd 移动速度

导入导出
* 导入素材可以直接放到 Assets 文件夹
* 导出素材，右键选择 Export Package，是 Unity 内部使用的压缩包

Shader（着色器）
* Material（材质）是由 Shader 实现的
* Shader 是比较高级的东西

【自己补充】修改 Unity Asset Store 下载位置的方法
* [[Unity]技巧分享：更改Unity Asset Store 默认下载资源位置的方法](https://errui.blog.csdn.net/article/details/112059936?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-112059936-blog-120874989.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-112059936-blog-120874989.pc_relevant_default&utm_relevant_index=1)

### 10 - 11
绘制贴图时需要先添加地形层

### 12 - 18
对象的各种属性功能由 Component（组件）决定

脚本类名和文件名要相同

生命周期方法
* `Awake()`
* `OnEnable()`
* `Start()`
* `FixedUpdate()`
* `Update()`
* `LateUpdate()`
* `Ondisable()`
* `OnDestroy()`

输出信息：`Debug.Log(字符串)`

脚本执行顺序
* Project Settings - Script Execution Order

### 19 - 23
C# 中，`0.5`默认是 double 类型，如果想要指定为 float，应该写`0.5f`

Debug
* 三种类型的 Debug 输出：`Debug.Log`，`Debug.LogWarning`，`Debug.LogError`
* 画线：`Debug.DrawLine(起点向量，终点向量，颜色)`，`Debug.DrawRay(起点向量，方向向量，颜色)`
	- 颜色形如`Color.Red`

获取当前脚本所挂载的游戏物体
* `GameObject go = this.gameObject;`

游戏物体的属性
* `go.name`，`go.tag`，`go.layer`
* 激活状态
	- `go.activeInHierarchy`：真正的激活状态（如果父物体非激活，该物体也为非激活）
	- `go.activeSelf`：自身激活状态
	- 设置激活状态：`go.SetActive(true 或 false);`
* 获取组件
	- 获取 Transform 组件：`Transform trans = this.transform`，或者直接`transform`
	- 获取其他组件（以 BoxCollider 为例）：`BoxCollider bc = GetComponent<BoxCollider>();`
		+ 泛型
	- 获取子物体的组件：`GetComponentInChildren<CapsuleCollider>(bc);`
	- 获取父物体的组件：`GetComponentInParent<BoxCollider>();`
	- 添加组件：`Cube.AddComponent<AudioSource>();`
* 获取游戏物体
	- 通过名称获取：`GameObject test = GameObject.Find("Test");`
	- 通过名称获取：`GameObject test = GameObject.FindWithTag("Enemy");`
* 销毁：`Destroy(go)`

通过预制件生成对象
1. 获取预制件：`public GameObject Prefab;`
	- 在编辑器中拖过来
2. 实例化游戏物体：`Instantiate(Prefab);`

### 24 - 27
Unity 中的各种类
* Time：游戏时间相关
* Application：数据访问权限（如获取文件夹位置等）
	- 后台运行： Project Settings - Player - Resolution and Presentation - Run In Background

多场景
* 在 Assets/Scene 文件夹下创建场景后，需要将场景拖进 File - Build Settings - Scenes In Build 中

### 28 - 31
游戏物体的父子关系是 Transform 维持的

Transform 的 Local Position（`transform.localPosition`）是相对父物体的位置

一般：z 轴是前方，x 轴是右方，y 轴是上方

虚拟轴
* 线性轴，\[-1, 1\]
* 具有兼容性
* 在 Project Settings - Input Manager 里设置对应的按键

### 32 - 35 灯光，摄像机，声音
让物体支持 Baked 形式的灯光
* 在 Inspector 右上角的 Static 旁点击，勾选 Contribute GI（GI 是 Global Light）
* 在 Window - Rendering - Lighting

相机的 Clear Flags：拍摄不到的地方用什么填充
* Depth Only：用于多相机叠加。相机有深度信息，从深度高的相机开始显示，拍摄不到的地方显示下一级相机的内容，以此类推

相机具有 Clipping Planes，一个 Near 一个 Far，只有两个面之间的物体才能被拍摄到

Render Texture
* 新建 Render Texture 资源，将相机的 Target Texture 设为该对象，则相机拍摄到的画面被传入该纹理资源中

Audio Listener（在 Camera 里）只能有一个

插入视频
* 游戏对象添加 Video Player 组件
* 设置源
* Render Mode 设为 Render Texture
* 将 Target Texture 设为某个 Render Texture（同前），视频就被渲染到材质上
* 将游戏对象的材质设为渲染材质

### 36 - 44 视频播放，物理，杂项（射线粒子拖尾）
控制角色的三种方案
1. 别人已有的资源
2. Unity 自带的角色控制器组件（Character Controller）
	- 仍然需要自己写部分脚本，但不涉及编写物理系统
3. 自己写

将相机放到当前 Scene 的视角
1. 选中摄像机
2. 菜单栏 Game Object - Align With View（`Ctrl+Shift+F`）

Character Controller 和 Rigidbody 不兼容（前者自带）

和 Character Controller 有关的问题
* 给 Player 挂载 Character Controller 组件和控制移动的脚本，脚本有如下代码：
	```c#
	player.SimpleMove(dir*5);
	// transform.Translate(dir * 5 * Time.deltaTime);
	```
	如果使用前一种方法，角色可以正常受重力下落；
	如果注释掉前一句改为后一种写法，角色却不会下落
* 使用 Character Controller，角色和其他 Rigidbody 碰撞不会撞倒
	但角色使用 Rigidbody 的话，会

Unity 取消脚本勾选后还会运行
* [Unity3D 挂载的脚本取消勾选居然还会运行！！](https://www.jianshu.com/p/7a680771c34b)

将碰撞器的 Is Trigger 勾选后，物体不会产生碰撞效果（会穿过去）

注意：碰撞和触发的函数，参数类型不一样
* 碰撞（如`OnCollisionEnter`）的参数类型为 Collision
* 触发（如`OnTriggerEnter`）的参数类型为 Collider

### 45 - 53 动画
使用 Animator 时，动画资源 Animation 创建在 Assets 里，但是需要挂到对象上才能用

fbx 文件的动画类别（在 Rig 栏里）
* Generic：泛型，通用
* Humanoid：人形动画，方便套用在别的人物模型上

Apply Root Motion 和 Bake into Pose
* 前者在游戏物体的 Animator 组件中，后者在 fbx 文件的 Animation 中，有 Rotation 和 Transform Y、Transform XZ 三种
* 前者把动画的移动放到绝对坐标下的 Transform，后者把移动放到相对坐标下的姿势

Curve
* 需要添加 Curve，以及在 Animator 界面添加参数（Float）

Event
* 事件的函数需要自己在脚本中写
* 当动画运行到事件时，会调用该名称的函数

混合动画
* Blend Tree
* 用参数控制动画的占比（例如从走到跑的线性动画）

有状态机父子，有多图层
* 多图层有权重覆盖，类似混合动画
* 可以对图层设置 Avatar Mask，遮罩人物（例如某图层动画只播放手臂部分）

反向动力学
* 力不是从手臂到手，而是从手到手臂
* 实现人物一直指向某物体的效果
* 需要在 Layer 里勾选 IK Pass

### 54 - 58 导航
1. 在 Inspector 右上角的 Static Checkbox 中设置 Navigation Static
2. Window - AI - Navigation 打开导航栏，设置限制，然后 Bake 生成导航网格
3. 给需要导航的物体添加 Nav Mesh Agent 组件

Obstacle Avoidance
* Priority：多个物体同时导航，谁先过障碍

\#BUG 失败了（"SetDestination" can only be called on an active agent that has been placed on a NavMesh.）

网格链接
* Generate OffMeshLink，对多个对象勾选，然后在 Bake 里设置 Drop Height 和 Jump Distance
* 或者在对象组件中添加 Off Mesh Link 组件

导航区域
* 不同区域可以设置不同的花费，都能走，但是费用不一样

### 59 - 66 UI
UI 基础物体：画布（Canvas），会自动创建 Event System
* 渲染模式 Render Mode：Overlay 是 UI 绝对覆盖摄像机画面，其他取决于物体距离
* UI 缩放模式 UI Scale Mode

Text
* 旧版
	- Rich Text：用 html 写法
* 新版
	- 功能更丰富
	- 导入 TMP Essential，大概 5 Mb

按钮事件
* 脚本可以挂载到任何物体上
* 设置事件时，选择脚本所挂载的物体，并在下拉列表里找到对应函数

文本输入框在旧版里

选项 Toggle
* 如果选项之间需要联动（例如性别不能都选），需要添加 Toggle Group 组件

下拉列表 Dropdown
* 如果需要添加选项图像，需要修改 Template，在其中添加 Image 组件，然后把该组件关联（拖动）到 Dropdown 的 Item Image 上，最后再为每个选项设置图片（这里是 Sprites）
* 标题图像同理，不过 Image 不是添加到 Template 里，而是作为 Dropdown 的子对象就行

Scroll View
* 原理就是遮罩控件 Mask

有用的组件
* Content Size Fitter
* Horizontal Layout Group，Vertical Layout Group，Grid Layout Group
