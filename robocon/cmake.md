![[CMake_Practice.pdf]]

# 基础
每个cmake项目都有一个或多个CMakeLists.txt 文件，用于定义项目的构建规则、依赖关系、编译选项等。

1. 指定CMake的最低版本要求：
```cmake
cmake_minimum_required(VERSION <version>)
```
2. 定义项目的名称和使用语言
```cmake
project(<project_name> [<language>...])
#例如
project(MyProject CXX)
```
3. 指定要生成的可执行文件和源文件
```cmake
add_executable(<target> <source_files>...)
#例如
add_executable(MyExecutable main.cpp other_file.cpp)
```
4. 创建库和源文件
```cmake
add_library(<target> <source_files>...)
#例如
add_library(MyLibrary STATIC library.cpp)
```
5. 链接目标文件和其他库
```cmake
target_link_libraries(<target> <libraries>...)

target_link_libraries(MyExecutable MyLibrary)
```
6. 添加头文件搜索路径
```cmake
include_directories(<dirs>...)

include_directories(${PROJECT_SOURCE_DIR}/include)
```
7. 设置变量的值
```cmake
set(<variable> <value>...)

set(CMAKE_CXX_STANDARD 11)
```
8. 设置目标属性
```cmake
target_include_directories(TARGET target_name
                          [BEFORE | AFTER]
                          [SYSTEM] [PUBLIC | PRIVATE | INTERFACE]
                          [items1...])

target_include_directories(MyExecutable PRIVATE ${PROJECT_SOURCE_DIR}/include)
```
9. 安装规则
```cmake
install(TARGETS target1 [target2 ...]
        [RUNTIME DESTINATION dir]
        [LIBRARY DESTINATION dir]
        [ARCHIVE DESTINATION dir]
        [INCLUDES DESTINATION [dir ...]]
        [PRIVATE_HEADER DESTINATION dir]
        [PUBLIC_HEADER DESTINATION dir])

install(TARGETS MyExecutable RUNTIME DESTINATION bin)
```
10. 条件语句
```cmake
if(expression)
  # Commands
elseif(expression)
  # Commands
else()
  # Commands
endif()
```
11. 自定义命令
```cmake
add_custom_command(
   TARGET target
   PRE_BUILD | PRE_LINK | POST_BUILD
   COMMAND command1 [ARGS] [WORKING_DIRECTORY dir]
   [COMMAND command2 [ARGS]]
   [DEPENDS [depend1 [depend2 ...]]]
   [COMMENT comment]
   [VERBATIM]
)
```
# 变量和缓存
##### 普通变量
- 定义变量：
```cmake
set(MY_VAR "Hello World")
```
- 使用变量
```cmake
message(STATUS "Variable MY_VAR is ${MY_VAR}")
```
##### 缓存变量
存储在CMake的缓存文件中，通常用于用户输入的设置
- 定义缓存变量
```cmake
set(MY_CACHE_VAR "DefaultValue" CACHE STRING "A cache variable")
```
- 使用缓存变量
```cmake
  message(STATUS "Cache variable MY_CACHE_VAR is ${MY_CACHE_VAR}")
```
# 查找库和包
find_packages()自动检测和配置外部库和包
```cmake
find_package(Boost REQUIRED)
find_package(Boost 1.70 REQUIRED)
#查找并指定路径
find_package(OpenCV REQUIRED PATHS /path/to/opencv)
#使用查找到的库
target_link_libraries(MyExecutable Boost::Boost)
#设置包含目录和链接目录
include_directories(${Boost_INCLUDE_DIRS})
link_directories(${Boost_LIBRARY_DIRS})
```
# CMake构建流程
1. **创建构建目录**：保持源代码目录整洁。
将构建文件放在源代码目录以外的独立目录中，保证源代码目录的整洁并方便管理
在项目的根目录下创建一个新的构建目录。例如，可以创建一个名为 build 的目录。
进入
2. **使用 CMake 生成构建文件**：配置项目并生成适合平台的构建文件。
- 运行 CMake 配置: 在构建目录中运行 CMake 命令，指定源代码目录。源代码目录是包含 CMakeLists.txt 文件的目录。
>如果需要指定生成器（如 Ninja、Visual Studio），可以使用 -G 选项.
>如果需要指定构建类型（如 Debug 或 Release），可以使用 -DCMAKE_BUILD_TYPE 选项。

- 检查配置结果: CMake 会输出配置过程中的详细信息，包括找到的库、定义的选项等，如果没有错误，构建系统文件将被生成到构建目录中。
3. **编译和构建**：使用生成的构建文件执行编译和构建。
>-  使用生成的构建文件进行编译和构建，不同的构建系统使用不同的命令
>- 如果使用Ninja系统，运行ninja命令来编译和构建项目
>```cmake
>ninja MyExecutable
>```
4. **清理构建文件**：删除中间文件和目标文件。
>构建过程中生成的中间文件和目标文件可以删除
>```cmake
>ninja clean
>```
5. **重新配置和构建**：处理项目设置的更改。
>cmake . .

# CMake构建实例
```项目结构
MyProject/
├── CMakeLists.txt
├── src/
│   ├── main.cpp
│   └── mylib.cpp
└── include/
    └── mylib.h
```
>`main.cpp`：主程序源文件。
>`mylib.cpp`：库源文件。
>`mylib.h`：库头文件。
>`CMakeLists.txt`：CMake 配置文件。

1. **创建 `CMakeLists.txt` 文件**：定义项目、目标和依赖。
```cmake
cmake_minimum_required(VERSION 3.10)   # 指定最低 CMake 版本为3.10

project(MyProject VERSION 1.0)          # 定义项目名称为MyProject和版本为1.0

# 设置 C++ 标准为 C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 添加头文件搜索路径
include_directories(${PROJECT_SOURCE_DIR}/include) #指定头文件目录

# 添加源文件
add_library(MyLib src/mylib.cpp)        # 创建一个库目标 MyLib，源文件是mylib.cpp
add_executable(MyExecutable src/main.cpp)  # 创建一个可执行文件目标 MyExecutable，源文件是main.cpp

# 链接库到可执行文件
target_link_libraries(MyExecutable MyLib) #将 MyLib 库链接到 MyExecutable 可执行文件。
```
2. **创建构建目录**：保持源代码目录整洁。
>打开终端，进入 MyProject 目录，然后创建构建目录：
>```bash
>mkdir build
cd build
>```
3. **配置项目**：使用 CMake 生成构建系统文件。
>在构建目录中使用 CMake 配置项目，这将生成适合平台的构建系统文件如 Makefile。
>在构建目录中运行CMake配置命令：
>```
>cmake .. #..指向源代码目录，即包含 `CMakeLists.txt` 文件的目录。CMake 将读取 `CMakeLists.txt` 文件并生成构建系统文件。
>```
4. **编译项目**：使用构建系统文件编译项目。
>使用生成的构建系统文件编译项目，根据生成的构建系统文件类型使用相应的构建命令
>若生成了Makefile，可以使用make命令进行编译
>```
>make  #make编译项目并生成可执行文件MyExecutable
>```
5. **运行可执行文件**：执行生成的程序。
>在构建目录中，运行MyExecutable
>```
>./MyExecutable
>```
6. **清理构建文件**：删除中间文件和目标文件。
```
make clean
```
# 高级特性
