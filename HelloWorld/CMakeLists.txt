# #cmake的版本
# cmake_minimum_required(VERSION 2.8)
# project(Point)

# #设置为release版本
# SET(CMAKE_BUILD_TYPE Release)

# #设置生成可执行文件和链接库保存的路径
# set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

# #设置头文件目录
# include_directories(
# ${PROJECT_SOURCE_DIR}/include
# )

# #选择需要编译的源文件
# add_executable(Point src/point.cpp src/main.cpp)

#1.cmake verson，指定cmake版本 
cmake_minimum_required(VERSION 3.5)

#2.project name，指定项目的名称，一般和项目的文件夹名称对应
PROJECT(HelloWorld)

#设置编译器（可选的有gcc，g++）
SET(CMAKE_CXX_COMPILER "g++")     

# 设置用debug还是release模式。debug允许断点，而release更快
set( CMAKE_BUILD_TYPE Debug )
#set( CMAKE_BUILD_TYPE Release )

#设置支持gdb调试
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g2 -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")


# 设置编译选项
# 允许c++11标准、O3优化、多线程。match选项可避免一些cpu上的问题
set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -march=native -O3 -pthread" )

#设置为release版本
#SET(CMAKE_BUILD_TYPE Release)

#设置生成可执行文件和链接库保存的路径
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#set(CMAKE_CXX_STANDARD 11)#c++11
#set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)
#3.head file path，头文件目录
INCLUDE_DIRECTORIES(
${PROJECT_SOURCE_DIR}/include
)
#add_library(${PROJECT_NAME}  src/b.c)#添加为库文件

#4.source directory，源文件目录
AUX_SOURCE_DIRECTORY(src DIR_SRCS)

#5.set environment variable，设置环境变量，编译用到的源文件全部都要放到这里，否则编译能够通过，但是执行的时候会出现各种问题，比如"symbol lookup error xxxxx , undefined symbol"
SET(TEST_MATH  ${DIR_SRCS})

#6.add executable file，添加要编译的可执行文件
ADD_EXECUTABLE(${PROJECT_NAME} ${TEST_MATH})

#7.add link library，添加可执行文件所需要的库，比如我们用到了libm.so（命名规则：lib+name+.so），就添加该库的名称
TARGET_LINK_LIBRARIES(${PROJECT_NAME} m)

