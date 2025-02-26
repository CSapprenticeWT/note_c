# Step 1 : A Basic Starting Point

​	这个阶段我们将简单介绍一些`CMake`的基本语法，命令和变量。介绍完这些概念以后，将通过三个连接构建一个简单的CMake项目。

​	每个练习都会提供一定的背景信息，然后提供目标和资源列表。需要编辑的CMakeLists文件放在Step1文件夹下，并且包含一个或多个TODO，每个TODO需要用一两行代码完成。这些TODO应该按照顺序完成。`Getting Started`指导和提示你完成练习。然后`Build and Run`将会一步一步教你构建和测试项目。最后每个练习都会讨论预期结果。

​	**注意：**每一步都应该在上一步的基础上完成。

## Exercise 1 - Build a Basic Project

​	最基本的`CMake`项目都是通过单个源码文件来构建可执行程序的，构建这样一个简单的项目，只需要在`CMakeLists.txt`中写入三条命令。

​	**注意：**虽然`CMake`支持大写、小写或混合大小写命令。但是推荐使用小写命令，并且本教程也将使用小写命令。

​	任何项目的顶层 `CMakeLists.txt` 文件必须以 `cmake_minimum_required()` 命令开始，来指定最低支持的 CMake 版本。这一命令用于设置相关策略，确保接下来的 CMake 函数在兼容的 CMake 版本中运行。

​	启动一个项目时，我们使用 `project()` 命令设置项目名称。该命令是每个项目都必须调用的，并且应尽早放置在 `cmake_minimum_required()` 命令之后。正如我们稍后会看到的，该命令还可以用来指定其他项目级信息，例如编程语言或版本号。

​	最后，`add_executable()` 命令用于告诉 CMake 创建一个可执行文件，并指定对应的源代码文件。

```cmake
# TODO 1: Set the minimum required version of CMake to be 3.10
cmake_minimum_required(VERSION 3.10)

# TODO 2: Create a project named Tutorial
project(Tutorial)

# TODO 3: Add an executable called Tutorial to the project
# Hint: Be sure to specify the source file as tutorial.cxx
add_executable(Tutorial tutorial.cxx)
```

### 编译和运行

```shell
mkdir build
cd build
cmake ../Step1		# 配置项目
cmake --build . 	# 构建项目
Tutorial 4294967296	# 运行项目
Tutorial 10
Tutorial
```

> 这里的配置项目的主要目的是以下几个步骤：
>
> 1. 定位CMakeLists.txt文件 -> 定义项目环境，检查文件结构，检查依赖etc.
> 2. 检测工具链和系统信息  -> 编译器，目标平台（操作系统），构建工具（Ninja，Visual Studio，Makefile）
> 3. 生成构建系统文件

## Exercise 2 - Specifying the C++ Standard

​	添加指定`c++11`的命令，完成步骤4-步骤6。

​	添加`c++11`特性，在`tutorial.cxx`中替换`atof`为`std::stod`。

```c++
// A simple program that computes the square root of a number
#include <cmath>
#include <cstdlib> // TODO 5: Remove this line
#include <iostream>
#include <string>

// TODO 11: Include TutorialConfig.h

int main(int argc, char* argv[])
{
  if (argc < 2) {
    // TODO 12: Create a print statement using Tutorial_VERSION_MAJOR
    //          and Tutorial_VERSION_MINOR
    std::cout << "Usage: " << argv[0] << " number" << std::endl;
    return 1;
  }

  // convert input to double
  // TODO 4: Replace atof(argv[1]) with std::stod(argv[1])
  const double inputValue = atof(argv[1]);
  // const double inputValue = std::stod(argv[1]);

  // calculate square root
  const double outputValue = sqrt(inputValue);
  std::cout << "The square root of " << inputValue << " is " << outputValue
            << std::endl;
  return 0;
}

```



