cmake_minimum_required(VERSION 3.10)
project(AngleTriangleDemo)

set(CMAKE_CXX_STANDARD 17)

# 添加 glad 的源文件和头文件路径
include_directories(include)
add_executable(${PROJECT_NAME} main.cpp src/glad.c)

# 查找并链接 GLFW
find_package(glfw3 REQUIRED)
target_link_libraries(${PROJECT_NAME} glfw)

# 链接 macOS 框架
target_link_libraries(${PROJECT_NAME} "-framework Foundation" "-framework IOKit" "-framework CoreVideo" "-framework Cocoa" "-framework Carbon")

# 关键：链接 ANGLE 库
# 设置 rpath，让可执行文件在运行时能找到同目录下的 dylib
set(CMAKE_INSTALL_RPATH "@executable_path")
set(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
target_link_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/angle_libs)
target_link_libraries(${PROJECT_NAME} libEGL.dylib libGLESv2.dylib)