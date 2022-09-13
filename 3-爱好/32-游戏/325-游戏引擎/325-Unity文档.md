# Unity文档
内容：对于Unity官方文档的阅读笔记
Unity版本：2021.3.1f1c1
文档版本：2021.1（中文）

## 三、在Unity中操作
### 3.3 Unity的界面
#### 3.3.2 Scene视图
##### Scene视图导航
按住`Shift`，点击场景视图辅助图标（Scene Gizmo，右上角的xyz正方体）：返回**透视图**（Perspective），且使用从侧面和略微从上方观察的角度查看场景

可以按`Alt`键配合左键旋转视角，右键缩放

飞越模式（Flythrough mode）中可以通过鼠标滚轮快速调节移动速度

##### 拾取和选择游戏对象
设置在场景（Scene）中是否可以选择对象。单击切换该项及其子项的可拾取性，按住`Alt`再单击只影响当前对象
![拾取和选择游戏对象](../../../img/2022-04-29_19-05-39_Unity-场景可拾取性.png)

##### 游戏对象定位
移动时按住`Shift`：在视图摄像机面向方向的平面上移动

Pivot 和 Center 的区别：Pivot 由模型指定，Center 由 Unity 根据对象的物理属性计算得到

对齐
* 移动和旋转时，按住`Ctrl`，按住`Shift+Ctrl`都有相应效果
* 移动时按住`v`键进入顶点对齐模式，也可以按`Shift+v`切换

##### 场景可见性
类似可拾取性

Isolation视图
* 选中一些对象，按`Shift+H`，这些对象将被隔离到单独的视图中

##### Scene视图控制栏
##### Gizmos菜单
辅助图标

#### 3.3.3 Game视图
#### 3.3.4 Hierarchy窗口
#### 3.3.5 Inspector窗口
检查多个项：
* 会显示共有的属性
* 相同的属性，显示实际值
* 不同的属性，显示破折号

##### 专属Inspector
右键某个对象，选择 Properties

#### 3.3.6 编辑属性
属性分为两种：
1. 引用
2. 值

### 3.4 Quickstart guides
#### 3.4.1 3D game development quickstart guide
##### Creating a 3D game
Fundamentals
* GameObjects
* Scenes
* Components：behavior of GameObjects
	- Transform
	- Mesh Fliter：网格
	- Mesh Renderer：网格贴图
	- Cameras
	- Rigidbody
	- Colliders

Scripts

3D Assets
* 导入格式：.fbx（或其他格式，导入后 Unity 会转为 .fbx）

Building in-game environments

Animation

Graphics

User Interface

### 3.5 创建游戏玩法
#### 3.5.1 场景
##### 创建、加载和保存场景
从C#脚本创建一个新场景
```c#
Tuple<Scene, SceneAsset> SceneTemplate.Instantiate(SceneTemplateAsset sceneTemplate, bool loadAdditively, string newSceneOutputPath = null);
```

#### 3.5.2 游戏对象
##### 变换组件（Transform）
每个游戏对象都有

包括三个属性
* Position
* Rotation
* Scale
	- 原始大小为1

父子化
* Inspector 中任何子游戏对象的 Transform 值都是相对于父项 Transform 值显示的结果

非一致缩放的限制
* 有些组件（例如由 radius 定义的球）不完全支持非一致缩放
* 在父子化时非一致缩放有时会出现问题

缩放比例的重要性
* 太大会影响性能（Unity 中网格有单位长度，物理引擎假定单位长度为 1m）

##### 组件简介
其他常用组件
* Main Camera
* Rigid Body

##### 使用组件
有些组件之间会互相依赖（例如 Hinge Joint 和 Rigidbody）

可以在运行时修改组件的参数用于测试，运行后将恢复原来的值

##### 原始对象和占位对象
原始对象
* Cube
	- 边长为 1
* Sphere
	- 直径为 1
* Capsule
	- 直径为 1，高度为 2
* Cylinder
	- 直径为 1，高度为 2
	- 注意碰撞体实际是胶囊体
* Plane
	- 在 XZ 平面
	- 边长为 10
	- 包含两百个三角形
* Quad
	- 在 XY 平面
	- 边长为 1
	- 分为两个三角形
	
##### 标签
可用于脚本

使用例：通过设置 GameObject.FindWithTag() 函数，可以查找包含所需标签的游戏对象。以下示例便使用了 GameObject.FindWithTag()。该函数在具有“Respawn”标签的游戏对象位置实例化 respawnPrefab：
```c#
using UnityEngine;
using System.Collections;

public class Example : MonoBehaviour {
    public GameObject respawnPrefab;
    public GameObject respawn;
    void Start() {
        if (respawn == null)
            respawn = GameObject.FindWithTag("Respawn");

        Instantiate(respawnPrefab, respawn.transform.position, respawn.transform.rotation) as GameObject;
    }
}
```

**只能为游戏对象分配一个标签**

Unity 包含一些未出现在标签管理器中的内置标签：
* Untagged
* Respawn
* Finish
* EditorOnly
* MainCamera
* Player
* GameController

##### 静态游戏对象
如果游戏对象在运行时未移动，则被称为静态游戏对象。如果游戏对象在运行时移动，则被称为动态游戏对象

提高性能

##### 保存工作
场景更改和项目范围内的更改是分开的

#### 3.5.3 预制件（prefabs）
理解为：对象的模板，在游戏运行前存在，在运行时可以实例化，是可重用资源

##### 创建预制件
将对象从 Hierarchy 窗口拖入 Projects 窗口
* 原始的游戏对象也会被转化为实例

##### 在预制件模式下编辑预制件
可以单独编辑，或者在上下文中编辑

撤销只在编辑中生效，一旦退出编辑就不能撤销

##### 实例覆盖
对预制件的修改会修改所有实例

直接对单个实例进行修改，会在该实例上创建实例覆盖

四种覆盖类型
* 覆盖属性的值
* 添加组件
* 删除组件
* 添加子游戏对象

覆盖优先于预制件的值

**对齐**不会从预制件传递到实例

##### 预制件变体
创建方法
* Project 窗口，右键单击，`Create > Prefab Variant`

\#TODO 没有理解

##### 解压缩预制件实例
选择`Prefab > Unpack`可以解压缩预制件实例，效果为：实例变为普通对象，和预制件不再有关系（但是对象的各种属性没有改变）

#### 3.5.4 层
层用于分隔游戏对象和功能，定义了哪些游戏对象可以与不同的功能以及彼此交互。
常见用途：
* 摄像机仅渲染场景的一部分
* 光源仅照亮场景的一部分
* 供射线投射用于选择性地忽略碰撞体或创建碰撞

创建新层：
* Edit > Project Settings，然后选择 Tags and Layers
* 有一部分默认层，其他可以自行指定（命名）

指定对象的层
* 层是对象的属性，可以在 Inspector 的 Layer 里修改

修改摄像机的剔除遮罩
* 在 Camera 的 Culling Mask 里选择要渲染的层
* 屏幕空间画布子项（UI 元素）会不受摄像机的剔除遮罩影响

选择性投射光线
* 对于投射光线函数`Physics.Raycast(transform.position, Vector3.forward, Mathf.Infinity, layerMask)`，layerMask 按位获取掩码（如果第 x 位为 0，则第 x 层被忽略）
* 不传 layerMask 参数时，默认只忽略 IgnoreRaycast 层的碰撞体

##### 基于层的碰撞检测
Edit > Project Settings，然后选择 Physics，最下面可以设置层碰撞矩阵（决定层两两之间是否允许碰撞）

#### 3.5.5 约束
将游戏对象的位置、旋转或缩放（也就是 Transform）与另一个相关联

约束是组件（Component），在其 Sources 列表中可以指定要关联的游戏对象
* 当关联多个对象时，取平均位置
* Sources 列表的顺序会影响 Parent Constraint、Rotation Constraint 和 Aim Constraint 组件
* 避免创建循环约束

##### 目标约束 (Aim Constraints)
##### Look At 约束 (Look At Constraints)
##### 父约束 (Parent Constraints)
##### 位置约束 (Position Constraints)
##### 旋转约束 (Rotation Constraints)
##### 缩放约束 (Scale Constraints)
#### 3.5.6 Unity 中的旋转和方向
内部采用四元数，Inspector 中采用等效欧拉角

#### 3.5.7 光源

#### 3.5.8 摄像机
#### 3.5.9 跨平台注意事项
#### 3.5.10 发布构建
File > Build Settings

#### 3.5.11 故障排除
### 3.6 编辑器功能
#### 3.6.1 2D 和 3D 模式设置
顶部菜单：`Edit > Project Settings`，然后选择 Editor 类别，将 Default Behavior Mode 设置为 2D 或 3D

### 3.6.2 Preference
### 3.6.3 Shortcuts Manager

## 十、脚本
### 10.2 脚本概念
#### 10.2.1 创建和使用脚本
为了连接到 Unity 的内部架构，脚本将**实现一个类**，此类从称为 MonoBehaviour 的内置类**派生**而来。

类名和文件名必须相同才能使脚本组件附加到游戏对象

两个函数
* 在游戏开始之前（即第一次调用 Update 函数之前），Unity 将调用 Start 函数
* Update 函数是放置代码的地方，用于处理游戏对象的帧更新。

对象的构造由编辑器处理，不会在游戏运行过程开始时进行。

将消息输出到控制台的函数：`Debug.Log("Hello world!");`

#### 10.2.2 变量和Inspector
将变量声明为 public，就可以在 Inspector 中查看和修改
* 仅在显示上，Inspector 中按驼峰命名法添加空格将变量名转化为词组

## 临时笔记

Q：写脚本时，如何引用脚本对应的对象？
A：使用GameObject类的方法`GetComponent`。例如将对象中 Renderer 的 Material 颜色设为红色，代码为：`GetComponent<Renderer>().material.color = Color.red;`

Q：如何修改 3D 对象的颜色？
A：Unity 中 3D 对象的外观是由材质（Material）确定的，修改颜色本质上是修改材质，或者添加不同的材质。
如果只是想要修改颜色，一种方法是创建若干不同的材质，在设置对象材质时选择需要的；
另一种方法是为对象设置修改颜色的脚本，在运行时为对象的**实例**单独设置颜色。例如：
```c#
public Color material_color;
void Start() {
    GetComponent<Renderer>().material.color = material_color;
}
```

Q：版本管理？
A：有以下几点需要注意：
1. 只管理 Assets 和 ProjectSettings 两个文件夹
2. 保证此设置：Edit > Project Settings > Editor > Asset Serialization 的 Mode 为 Force Text
