# Unity


## 未分类
### 获取对象
`transform.GetComponent<>()` 和 `transform.gameObject.GetComponent<>()` 好像都行

### 物理
#### Rigidbody
AddForce 的 mode 参数
1. ForceMode.Acceleration：施加加速度，不受
2. ForceMode.Force：
3. ForceMode.Impulse：
4. ForceMode.VelocityChange：

注
* 各种力都是持续一段时间
* 需要写在 FixedUpdate 里（因为 Rigidbody 是按 FixedUpdate 的固定时间算的）

### 使用 Excel
[【Unity教程】Excel文件的读取和写入 (使用EPPlus)](https://www.bilibili.com/video/av61819650)

打开，读取，修改和保存已存在的 Excel 文件
1. using OfficeOpenXml
2. 文件路径
3. 创建 ExcelPackage 对象
    - 注意 FileInfo 的使用需要 using System.IO
    - 使用 `using (ExcelPackage excelPackage = new ExcelPackage(fileInfo)) {...}`，using结束后，using 的资源会被释放
4. 使用 `excelPackage.Workbook.Worksheets[i]` 访问第 i 张 sheet，从 1 开始
5. 使用 `worksheet.Cells[i, j].Value.ToString()` 访问 i 行 j 列的单元格数据
    - 注意 C# 的多维数组是这样的
6. `excelPackage.Save()` 保存文件

创建 Excel 文件
1. ... FileInfo
2. using ... new ...
3. Worksheets.Add("表名") 添加 sheet

备注
* 这个插件包含了文件读写的部分，不需要自己实现；而 LitJson 包含了内置数据类型（JsonData）和字符串的转换，文件读写需要自己做

### 使用中文
### 使用协程
> 协程就像一个函数，能够暂停执行并将控制权返还给 Unity，然后在指定的时间继续执行。
> 协程本质上是一个用返回类型 IEnumerator 声明的函数，并在主体中的某个位置包含 yield return 语句。
> yield return 是暂停执行并随后在下一个时间点恢复。

\#TODO WaitWhile，WaitUntil

Unity 中的协程使用，需要在 MonoBehaviour 类上（例如 StartCoroutine 函数），且**使用协程的类必须挂载到游戏对象上**

## 杂项
### Unity Hub 创建项目时强制要求下载 Plastic SCM
登录就行了
