cmake_minimum_required(VERSION 3.20)
project(HelloCpp LANGUAGES CXX)

# C++17
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 生成 compile_commands.json 方便 LSP
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# ========= 目标 ========= #
# 1) 静态库 math 只包含 add.cc
add_library(math STATIC
    src/add.cc
)

# 让所有依赖 math 的目标都能找到头文件
target_include_directories(math PUBLIC
    ${CMAKE_SOURCE_DIR}/include
)

# 2) 可执行文件 hello
add_executable(hello
    src/main.cc
)

# 链接上前面的 math 库
target_link_libraries(hello PRIVATE math)
