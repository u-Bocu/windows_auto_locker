cmake_minimum_required(VERSION 3.24)
project(windows_auto_locker)

set(CMAKE_CXX_STANDARD 23)

# Set third party path
set(TFLite_PATH "C:/tensorflowlite")
set(TFLite_INCLUDE_DIRS "${TFLite_PATH}/include")
set(TFLite_LIBS "${TFLite_PATH}/libs/windows_x86_64/libtensorflowlite.so.if.lib")

add_executable(windows_auto_locker main.cpp machine_learning.cpp machine_learning.h main.cpp machine_learning.cpp machine_learning.h)

# Find opengl libraries
find_package(OpenCV REQUIRED)

# Add include path
target_include_directories(windows_auto_locker PRIVATE
        ${OpenCV_INCLUDE_DIRS}
        ${TFLite_INCLUDE_DIRS})

# Link libraries to app.
target_link_libraries(windows_auto_locker
        PRIVATE ${OpenCV_LIBS}
        PRIVATE ${TFLite_LIBS})

# Conditional compilation options
if(MSVC)
    target_compile_options(windows_auto_locker PRIVATE /MP)
endif()
