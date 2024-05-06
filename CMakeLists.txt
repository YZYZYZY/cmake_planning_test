cmake_minimum_required(VERSION 3.29.0)
project(Planning)
set(CMAKE_CXX_STANDARD 17)

#生成动态库
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin) #动态库和exe文件都指定到bin目录下面 Linux的不一样 静态库也不一样

aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)
#动态库
add_library(common
SHARED
${SRC_LISTS}
)
#包含头文件目录
target_include_directories(common
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

#生成可执行文件
add_executable(planning_main planning_main.cpp)

#包含头文件目录
target_include_directories(planning_main
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

#让可执行文件链接动态库
target_link_libraries(planning_main
PUBLIC
common
)