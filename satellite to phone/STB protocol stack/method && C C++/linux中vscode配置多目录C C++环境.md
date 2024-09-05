### **基于gcc/g++**
1. 工程目录(include, src)：
	.
	├── include
	│   └── functions.h
	└── src
	    ├── helloworld.cpp
	    ├── main.cpp
	    └── sum.cpp

2. 配置task.json
	终端 -> 配置默认生成任务
	更改args参数和options参数：
```cpp
"args": [
	"-fdiagnostics-color=always",
	"-g",
	"-I", //注意！否则编译时不会去include目录下找头文件
	"${workspaceFolder}/include",
	"${workspaceFolder}/src/\*.cpp",
	"-o",  
		// 这决定了可执行文件的输出位置，后面laucnh.json会用到	
	"${workspaceFolder}/bin/${fileBasenameNoExtension}"
],
"options": {
    "cwd": "${fileDirname}"
},
```

3. 配置launch.json
	运行 -> 添加配置 -> 选择C++(GDB/LLDB)

4. 更改C/C++配置
	ctrl + shift + p，找到编辑配置UI
	包含路径中添加:${workspaceFolder}/include