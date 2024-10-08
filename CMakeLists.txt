cmake_minimum_required(VERSION 3.15)

project(tst2 LANGUAGES CXX VERSION 1.0.0)

set(CMAKE_POSITION_INDEPENDENT_CODE TRUE)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)


#优先查找静态库
set(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
set(BUILD_SHARED_LIBS OFF)

# 关闭动态插件加载
set(QT_NO_DYNAMIC_CAST TRUE)

find_package(Qt6 COMPONENTS Core Widgets REQUIRED)
# 添加插件的静态库
find_package(Qt6 COMPONENTS QCocoaIntegrationPlugin REQUIRED)

add_executable(${PROJECT_NAME}
        src/main.cpp
        src/MyWindow.cpp
        src/MyWindow.h
)

set_target_properties(${PROJECT_NAME} PROPERTIES AUTOMOC ON)

find_library(METAL Metal)
find_library(QUARTZCORE QuartzCore)
find_library(IOSURFACE IOSurface)
find_library(CORESERVICES CoreServices)
find_library(UNIFORMTYPEIDENTIFIERS UniformTypeIdentifiers)

# 链接静态库
target_link_libraries(${PROJECT_NAME} PRIVATE
        Qt6::Widgets
        Qt6::Core
        Qt6::QCocoaIntegrationPlugin
        ${METAL}
        ${QUARTZCORE}
        ${IOSURFACE}
        ${CORESERVICES}
        ${UNIFORMTYPEIDENTIFIERS}
)

