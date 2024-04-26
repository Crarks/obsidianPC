vscode中
+ 下载安装g++ 即mingw
+ 配置mingw环境变量
+ cmd中g++ --version
+ c插件和run code之类
+ 在vscode中要运行c的话 要在运行文件夹下创建.vscode文件夹，其下放三个文件  
1. c_cpp_properties
```c
{
  "configurations": [
      {
        "name": "Win32",
        "includePath": ["${workspaceFolder}/**"],
        "defines": ["_DEBUG", "UNICODE", "_UNICODE"],
        "windowsSdkVersion": "10.0.17763.0",
        "compilerPath": "D:\\learn\\VScode TOOL\\mingw64\\bin\\g++.exe",   /*修改成自己bin目录下的g++.exe，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
        "cStandard": "c11",
        "cppStandard": "c++17",
        "intelliSenseMode": "${default}"
      }
    ],
    "version": 4}
```    
2. launch.json
```c
{
    // 使用 IntelliSense 了解相关属性。
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "g++.exe build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "D:\\learn\\VScode TOOL\\mingw64\\bin\\gdb.exe",      /*修改成自己bin目录下的gdb.exe，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "task g++"
        }
    ]
}
```
3.tasks.json
```c
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
        "type": "shell",
        "label": "task g++",
        "command": "D:\\learn\\VScode TOOL\\mingw64\\bin\\g++.exe", /*修改成自己bin目录下的g++.exe，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
        "args": [
            "-g",
            "${file}",
            "-o",
            "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "-I",
            "D:\\learn\\VScode TOOL\\C",      /*修改成自己放c/c++项目的文件夹，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
            "-std=c++17"
        ],
        "options": {
            "cwd": "D:\\learn\\VScode TOOL\\mingw64\\bin"   /*修改成自己bin目录，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
        },
        "problemMatcher":[
            "$gcc"
        ],
        "group": "build",
        }
    ]
}
```