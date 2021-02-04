---
title: vscode
date: 2021-02-04 16:23:25
tags: 奇技淫巧
---

在task里添加编译命令，从而执行编译操作。步骤如下：

  -  按住ctrl+shift+P，打开命令面板；
  -  选择Configure Tasks...，选择Create tasks.json file from templates，之后会看到一系列task模板；
  -  选择others，创建一个task，下面是一个task的示例：

<!--more-->

```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build hello world",     // task的名字
            "type": "shell",   
            "command": "g++",    //编译命令
            "args": [    //编译参数列表
                "-g", // 加上-g可以断点调试
                "main.cpp",
                "-o",
                "main.out"
            ]
        }
    ]
}
```
## 配置launch.json

把debug的内容配置在launch.json，这样我们就可以使用断点调试了。

  -  点击侧边栏的debug按钮，就是那只虫子图标；
  -  在上面的debug栏目里，点击齿轮图标；
  -  在下拉菜单中选择 C++ (GDB/LLDB)，这时会在.vscode文件夹下创建一个launch.json文件，用来配置debug；下面是launch.json文件的一个示例：

```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "debug hello world",    //名称
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/main.out",    //当前目录下编译后的可执行文件
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",    //表示当前目录
            "environment": [],
            "externalConsole": false, // 在vscode自带的终端中运行，不打开外部终端
            "MIMode": "gdb",    //用gdb来debug
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "build hello world"  //在执行debug hello world前，先执行build hello world这个task，看第4节
        }
    ]
}

```