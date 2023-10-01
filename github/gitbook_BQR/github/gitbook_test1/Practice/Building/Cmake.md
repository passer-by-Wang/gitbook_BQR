## CMakeList.txt下各命令功能

### 1、常用

```cmake
cmake_minimum_required(Version 3.0) #指定cmake最低版本，该值应该低于安装cmake版本
project(test VERSION 1.0.0 LAUGUAGES C CXX)  #指定项目名字、版本、语言（C代表C语言，CXX代表C++）
add_executable(test src/main.cpp)  #指定源文件，源文件可以有多个但是只能有一个main函数
```

### 2、编译方式

* (a)在CMakeList.txt所在目录下命令行模式

```cmake
cmake -B build  #在build下生成Makefile
cmake --build build
```

* (b)创建build，在build目录下执行

```cmake
cmake ..  #指定源文件目录-S，比如'cmake -S .'，
# 指定变量-D，比如'-DCMKAE_BUILD_TYPE=Debug DAUTHOR=RealCoolEngineer'
make  #Cmake是对大小写敏感的
```

### 3、Cmake内置变量

- CMAKE_BINARY_DIR,PROJECT_BINARY_DIR,_BINARY_DIR：这三个变量内容一致，如果是内部编译，就指的是工程的顶级目录，如果是外部编译，指的就是工程编译发生的目录。
- CMAKE_SOURCE_DIR,PROJECT_SOURCE_DIR,_SOURCE_DIR： 这三个变量内容一致，都指的是工程的顶级目录。
- CMAKE_CURRENT_BINARY_DIR: 外部编译时，指的是target目录，内部编译时，指的是顶级目录
- CMAKE_CURRENT_SOURCE_DIR: CMakeList.txt所在的目录
- CMAKE_CURRENT_LIST_DIR: CMakeList.txt的完整路径
- CMAKE_CURRENT_LIST_LINE: 当前所在的行
- CMAKE_MODULE_PATH: 如果工程复杂，可能需要编写一些cmake模块-，这里通过SET指定这个变量
- LIBRARY_OUTPUT_DIR,BINARY_OUTPUT_DIR: 库和可执行的最终存放目录

### 4、设置包含目录

```cmake
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_BINARY_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)
```

Linux下还可以通过flag的方式设置：

```CMAKE
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -I${CMAKE_CURRENT_SOURCE_DIR}")
```

该命令常常与其他命令组合使用

```cmake
find_package(Eigen3 3.3 REQUIRED NO_MODULE)
include_directories(
include
$(EIGEN3_INCLUDE_DIRS)
)
```

### 5、设置搜索目录

```cmake
link_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/libs64
)
link_directories(/home/test/myprojects/libs)
```

不建议使用该命令，而建议使用：

```CMAKE
target_link_libraries(${catkin_LIBRARIES}
)
```

### 6、链接库

```cmake
target_link_libraries(demo test)
```

它会自动在系统默认库路径和指定自定义库路径进行搜索libtest.a和libtest.so文件

**指定完整路径**

```cmake
target_link_libraries(demo ${CMAKE_CURRENT_SOURCE_DIR}/lib/test.so)
```

**指定多个链接库**

```cmake
target_link_libraries(demo 
    ${CMAKE_CURRENT_SOURCE_DIR}/libs64/libtest.a 
    pthread)
```

### 7、打印消息

```cmake
message([<mode>] "message text" ...)
```

1. 空或者`NOTICE`：比较重要的信息，如前面演示中的格式
2. DEBUG：调试信息，主要针对开发者
3. STATUS：项目使用者可能比较关心的信息，比如提示当前使用的编译器
4. WARNING：CMake警告，不会打断进程
5. SEND_ERROR：CMake错误，会继续执行，但是会跳过生成构建系统
6. FATAL_ERROR：CMake致命错误，会终止进程

### 8、包含子目录

```cmake
add_subdirectory (source_dir [binary_dir] [EXCLUDE_FROM_ALL])
```

- **`source_dir`**
  **必选参数**。该参数指定一个子目录，子目录下应该包含`CMakeLists.txt`文件和代码文件。子目录可以是相对路径也可以是绝对路径，如果是相对路径，则是相对当前目录的一个相对路径。

其他为可选参数

### 9、生成链接库

生成链接库

```cmake
add_library(hello SHARED test.cpp)
```

在上层文件中需要添加链接库的link

```cmake
add_executable(...)
target_link_libraries(demo hello)
```

### 10、Ctest和Cpack

待补充

### 11、环境变量

- 使用环境变量：`$ENV{Name}`
- 写入环境变量：`set(ENV{Name} value`) #这里没有“$”符号

### 12、系统信息

- CMAKE_MAJOR_VERSION，CMAKE 主版本号，比如2.4.6 中的2
- CMAKE_MINOR_VERSION，CMAKE 次版本号，比如2.4.6 中的4
- CMAKE_PATCH_VERSION，CMAKE 补丁等级，比如2.4.6 中的6
- CMAKE_SYSTEM ，系统名称，比如Linux-2.6.22
- CMAKE_SYSTEM_NAME ，不包含版本的系统名，比如Linux
- CMAKE_SYSTEM_VERSION ，系统版本，比如2.6.22
- CMAKE_SYSTEM_PROCESSOR，处理器名称，比如i686
- UNIX ，在所有的类UNIX平台为TRUE，包括OS X 和cygwin
- WIN32 ，在所有的win32 平台为TRUE，包括cygwin

### 13、开关选项

- `BUILD_SHARED_LIBS`： 用来控制默认的库编译方式，如果 不设置，使用`add_library`在没有指定库类型的情况下，默认生成的都是静态库。如果设置了`set(BUILD_SHARED_LIBS ON)`后，默认生成动态库。
- `CMAKE_C_FLAGS`设置C编译选项，也可以通过`add_definitions()`添加
- `CMAKE_CXX_FLAGS`设置C++编译选项，也可以通过指令`add_definitions()`添加。
- `option`可以添加cmake编译选项。

### 14、设置变量

#### 14.1、set直接设置变量的值

```cmake
set(SRC_LIST main.cpp test.cpp)
add_executable(demo ${SRC_LIST})
```

#### 14.2、set追加变量的值

```cmake
set(SRC_LIST main.cpp)
set(SRC_LIST ${SRC_LIST} test.cpp)
add_executable(demo ${SRC_LIST})
```

#### 14.3、list追加或删除变量的值

```cmake
set(SRC_LIST main.cpp)
list(APPEND SRC_LIST test.cpp)
list(REMOVE_ITEM SRC_LIST main.cpp)
add_executable(demo ${SRC_LIST})
```

### 15、条件控制

### if...else...elseif...endif

```cmake
if(MSVC)
    set(LINK_LIBS common)
else()
    set(boost_thread boost_log.a boost_system.a)
endif()

target_link_libraries(demo ${LINK_LIBS})

if(${CMAKE_BUILD_TYPE} MATCHES "debug")
    ...
else()
    ...
endif()
```

### while break continue foreach endwhile endforeach

```cmake
while(TRUE)
  message(STATUS "While true")
  break()
endwhile()

foreach(project_file ${COMMON_PROJECT_FILES})
        message(STATUS "project file found -- ${project_file}")
        include("${project_file}")
    endforeach()
```

### 16、其他

```cmake
aux_source_directory(. SRC_LIST) #搜索当前目录下的所有.cpp文件
file(GLOB SRC_LIST "*.cpp" "*.cc") #GLOB不支持递归遍历子目录，若想实现递归遍历子目录，请使用GLOB_RECURSE
```

**指定c和c++标准**

```cmake
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")  #设置c++的编译选项
set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99")  #设置c的编译选项
```

```cmake
set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 11)
```





