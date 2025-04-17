# Godot
## 操作
### 调试
使用 VSCode: 目前 (2023/8/29) 插件自带的模板有问题, Build 会在 VSCode 卡住, 无法继续, 但是 Godot Build 成功

将 `tasks.json` 和 `launch.json` 分别设置如下:

`tasks.json`
```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",
            "command": "dotnet",
            "type": "shell",
            "args": [
                "build",
                "/property:GenerateFullPaths=true",
                "/consoleloggerparameters:NoSummary"
            ],
            "group": "build",
            "presentation": {
                "reveal": "silent",
            },
            "problemMatcher": "$msCompile"
        }
    ]
}
```

`launch.json`
```json
{
    "version": "2.0.0",
    "configurations": [
        {
            "name": "Launch",
            "type": "coreclr",
            "request": "launch",
            "preLaunchTask": "build",
            "program": "d:\\Software\\Godot_v4.1.1-stable_mono_win64\\Godot_v4.1.1-stable_mono_win64.exe",
            "console": "internalConsole",
            "stopAtEntry": false
        }
    ]
}
```

## 问题
### VSCode
问题: 在 VSCode 中找不到命名空间 (如 Godot)
解决: 在 Godot 中的 MSBuild 选项 Build 一下

问题: 在 Godot 中添加信号, 只会跳转到外部编辑器 VSCode, 不会自动添加代码
解决: 暂无, 不设置外部编辑器就可以在用内部编辑器添加代码
更多: 在 VSCode 的 C# 提示中, _Ready() 等函数的 reference 数量似乎有误 (为 0, 但所看教程中不为 0)

问题: VSCode 中的 godot-tools 插件连接不到 Godot
解决: (可能) 确保 Godot 网络选择中的端口和插件设置的端口相同