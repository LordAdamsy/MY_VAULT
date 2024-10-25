编写CMakeLists.txt

```cmake
cmake_minimum_required(VERSION 3.16)
project(calculator)
message("CMAKE_SOURCE_DIR: ${CMAKE_SOURCE_DIR}")
message("PROJECT_SOURCE_DIR: ${PROJECT_SOURCE_DIR}")
set(INCLUDE_DIR ${PROJECT_SOURCE_DIR}/include)
#file(GLOB SRC_LIST "${CMAKE_SOURCE_DIR}/src/*.cpp")
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LIST)
message(${INCLUDE_DIR})
message(${SRC_LIST})
add_executable(main ${SRC_LIST})
target_include_directories(main PUBLIC ${INCLUDE_DIR})
message("Succeed!")
```

语法总结：

set(<variable> <value>) 设置变量

aux_source_directory(<dir> <variable>) 收集目录下所有的源文件到变量中

file(GLOB/GLOB_RECURSE <variable> <filepath>) 功能与上条类似，匹配方式更灵活，
GLOB_RECURSE支持目录递归查找

target_include_directories(<project_name> <INTERFACE|PUBLIC|PRIVATE>
<headfile_directory>) 指定所要包含的头文件。

message("your message") 在终端打印信息。