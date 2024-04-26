vscode中
+ 下载安装g++ 即mingw
+ 配置mingw环境变量
+ cmd中g++ --version
+ c插件和run code之类
+ 在vscode中要运行c的话 要在运行文件夹下创建.vscode文件夹，其下放三个文件  
    1. c_cpp_properties
    2. launch.json
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