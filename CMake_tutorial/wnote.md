# 一些其他用到的笔记

```cmake
cmake_minimum_required(VERSION 3.16)
project(MyProject)

# 设置项目根路径
set(PROJECT_ROOT ${CMAKE_CURRENT_SOURCE_DIR})
set(EMULIBS_HOME "${PROJECT_ROOT}/usr/emulibs/home")
set(EMULIBS_INCLUDE "${PROJECT_ROOT}/usr/emulibs/include")

# 收集所有 .a 库文件
file(GLOB_RECURSE EMULIBS_LIBRARIES
    "${EMULIBS_HOME}/**/*.a"
    "${EMULIBS_INCLUDE}/**/*.a"
)

# 收集所有头文件目录
file(GLOB_RECURSE EMULIBS_INCLUDE_DIRS
    "${EMULIBS_HOME}/**/"
    "${EMULIBS_INCLUDE}/**/"
)

# 去重，确保路径唯一
list(REMOVE_DUPLICATES EMULIBS_LIBRARIES)
list(REMOVE_DUPLICATES EMULIBS_INCLUDE_DIRS)

# 打印调试信息
message(STATUS "Detected external libraries: ${EMULIBS_LIBRARIES}")
message(STATUS "Detected external include directories: ${EMULIBS_INCLUDE_DIRS}")

# 设置全局变量供模块使用
set(ALL_EXTERNAL_LIBS ${EMULIBS_LIBRARIES} CACHE INTERNAL "All external libraries")
set(ALL_EXTERNAL_INCLUDES ${EMULIBS_INCLUDE_DIRS} CACHE INTERNAL "All external include directories")

# 添加所有模块子目录
add_subdirectory(usr/module1)  # 添加其他模块同理

```

