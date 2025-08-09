cmake_minimum_required(VERSION 3.10)
project(PageManagerLib)

message(STATUS "[PageManager]  PageManager CMake version: ${CMAKE_VERSION}")

file(GLOB_RECURSE SOURCES 
  "${CMAKE_CURRENT_LIST_DIR}/*.cpp"
  
)

# 排除不需要的文件（可选）
# list(FILTER SOURCES EXCLUDE REGEX ".*test.*")

# 创建静态库
add_library(PageManagerLib STATIC ${SOURCES})

# 设置C++标准（如果需要）
target_compile_features(PageManagerLib PUBLIC cxx_std_11)

message(STATUS "[PageManager]  ${CMAKE_SOURCE_DIR}")
# 设置包含目录
target_include_directories(PageManagerLib PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include>
    ${CMAKE_SOURCE_DIR}/../lv_port_linux/lvgl
)

# 创建导出集
#install(TARGETS PageManagerLib
#    EXPORT PageManagerLib-targets
#    ARCHIVE DESTINATION lib
#    LIBRARY DESTINATION lib
#    RUNTIME DESTINATION bin
#    INCLUDES DESTINATION include
#)

# 安装头文件（如果有的话）
#install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
#    DESTINATION include/PageManagerLib
#    FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"
#)

# 安装导出配置
#install(EXPORT PageManagerLib-targets
#    FILE PageManagerLib-config.cmake
#    NAMESPACE PageManagerLib::
#    DESTINATION lib/cmake/PageManagerLib
#)

# 方法1：通过find_package
# find_package(your_library REQUIRED)
# target_link_libraries(your_target your_library::your_library)

# 方法2：通过add_subdirectory直接包含
# add_subdirectory(path/to/your/library)
# target_link_libraries(your_target your_library)
# target_include_directories(你的目标 PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/lib/PageManager)