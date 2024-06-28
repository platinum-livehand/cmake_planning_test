cmake_minimum_required(VERSION 3.29.0)
project(planning)
set(CMAKE_CXX_STANDARD 17)

# Windows 平台下将动态库和exe都指定到bin目录下
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
# CMAKE_LIBRARY_OUTPUT_DIRECTORY Linux 平台下指定动态库的位置
# CMAKE_ARCHIVE_OUTPUT_DIRECTORY Linux 平台下指定静态库的位置

# 生成动态库
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)
add_library(common
SHARED
${SRC_LISTS}
)

# 为目标(动态库)添加包含目录
target_include_directories(common
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

# 生成可执行文件
add_executable(planning_main planning_main.cpp)

# 为目标(可执行文件)添加包含目录
target_include_directories(planning_main
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

# 为目标(可执行文件)链接依赖库文件
target_link_libraries(planning_main
PUBLIC
common
)