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
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

# 2) 可执行文件 hello
add_executable(hello
    src/main.cc
)

# 链接上前面的 math 库
target_link_libraries(hello PRIVATE math)

# ========= 单元测试（可选） ========= #
# enable_testing()
# add_executable(test_add tests/test_add.cc)
# target_link_libraries(test_add PRIVATE math)
# add_test(NAME add_tests COMMAND test_add)

