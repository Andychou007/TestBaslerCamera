cmake_minimum_required(VERSION 3.16)
project(TestBaslerCamera)

set(CMAKE_CXX_STANDARD 14)

set(PROJECT_NAME TestBaslerCamera)
include_directories("${PROJECT_BINARY_DIR}")

set(PYLON_ROOT "/opt/pylon")
include_directories("${PYLON_ROOT}/include")


set(QT_ROOT /home/andy/Qt5.14.0/5.14.0/gcc_64/)
set(Qt5Core_DIR ${QT_ROOT}/lib/cmake/Qt5Core)
set(Qt5_DIR ${QT_ROOT}/lib/cmake/Qt5)
set(Qt5Charts_DIR ${QT_ROOT}/lib/cmake/Qt5Charts)
set(Qt5Gui_DIR ${QT_ROOT}/lib/cmake/Qt5Gui)
set(Qt5Widgets_DIR ${QT_ROOT}/lib/cmake/Qt5Widgets)
set(Qt5OpenGL_DIR ${QT_ROOT}/lib/cmake/Qt5OpenGL)
set(QT_QMAKE_EXECUTABLE ${QT_ROOT}/bin/qmake)
set(CMAKE_PREFIX_PATH ${QT_ROOT}/lib/cmake)

set(Qt_LIBRARIES ${QT_ROOT}/lib)
find_package(Qt5Core REQUIRED)
find_package(Qt5Gui REQUIRED)
find_package(Qt5Charts REQUIRED)
find_package(Qt5Widgets REQUIRED)
find_package(Qt5OpenGL REQUIRED)

#find_package(Qt 5.14.0 REQUIRED)
#set(${PROJECT_NAME}_DEP_LIBRARIES)
#set(${PROJECT_NAME}_DEP_TARGETS)
#set(${PROJECT_NAME}_DEP_LIBRARY_DIRS)
#set(${PROJECT_NAME}_DEP_INCLUDE_DIRS)
#find_package(PkgConfig)

#include_directories(${QT_ROOT/include})

#set(opencv_INCLUDE_DIRS "/home/andy/Hero_BuiltRobot/install/x64-install/oss/include/opencv2")
#set(opencv_LIBRARIES "opencv_calib3d;opencv_core;opencv_dnn;opencv_features2d;opencv_flann;opencv_gapi;opencv_highgui;opencv_imgcodecs;opencv_imgproc;opencv_ml;opencv_objdetect;opencv_photo;opencv_stitching;opencv_video;opencv_videoio;opencv_aruco;opencv_bgsegm;opencv_bioinspired;opencv_ccalib;opencv_cvv;opencv_datasets;opencv_dnn_objdetect;opencv_dpm;opencv_face;opencv_fuzzy;opencv_hfs;opencv_img_hash;opencv_line_descriptor;opencv_optflow;opencv_phase_unwrapping;opencv_plot;opencv_quality;opencv_reg;opencv_rgbd;opencv_saliency;opencv_shape;opencv_stereo;opencv_structured_light;opencv_superres;opencv_surface_matching;opencv_text;opencv_tracking;opencv_videostab;opencv_viz;opencv_ximgproc;opencv_xobjdetect;opencv_xphoto")

#set(OpenCV_DIR "/home/david/software/opencv-2.4.13.6/build")
#set(OpenCV_INCLUDE_DIRS "/home/david/software/opencv-2.4.13.6/include")
#set(OpenCV_LIBRARIES "/home/david/software/opencv-2.4.13.6/build/lib")
#find_package(OpenCV 2.4.13 REQUIRED)

###配置opencv
set(OpenCV_DIR /home/andy/Hero_BuiltRobot/install/x64-install/oss/lib/cmake/opencv4/)
#set(OpenCV_INCLUDE_DIRS "/home/andy/Hero_BuiltRobot/install/x64-install/include")
#set(OpenCV_LIBRARIES "/home/andy/Hero_BuiltRobot/install/x64-install/lib")
find_package(OpenCV 4.1.0 REQUIRED)
include_directories(${opencv_INCLUDE_DIRS})

###配置pylon
EXEC_PROGRAM("${PYLON_ROOT}/bin/pylon-config" ARGS --cflags OUTPUT_VARIABLE CPPFLAGS)
#SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${CPPFLAGS}" CACHE STRING "CPPFLAGS")
SET(CPPFLAGS "${CPPFLAGS}" CACHE STRING "CPPFLAGS")
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${CPPFLAGS}")

EXEC_PROGRAM("${PYLON_ROOT}/bin/pylon-config" ARGS --libs-rpath OUTPUT_VARIABLE LDFLAGS)
#SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${LDFLAGS}" CACHE STRING "LDFLAGS")
SET(LDFLAGS "${LDFLAGS}" CACHE STRING "LDFLAGS")
SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${LDFLAGS}")

EXEC_PROGRAM("${PYLON_ROOT}/bin/pylon-config" ARGS --libs OUTPUT_VARIABLE LDLIBS)
SET(LDLIBS "${LDLIBS}" CACHE STRING "LDLIBS")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")

add_executable(${PROJECT_NAME} main.cpp)


target_link_libraries(${PROJECT_NAME} ${LDLIBS})
#target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS})
target_link_libraries(${PROJECT_NAME} ${Qt_LIBRARIES})


##指定cmake的最小版本号
##CMAKE_MINIMUM_REQUIRED(VERSION 3.16)
##指定项目名称
##PROJECT(Arithmetic LANGUAGES CXX)
##指定Qt路径和启用当前目录(按需设置)
#SET(CMAKE_PREFIX_PATH ${QT_PATH}/lib/cmake)
#SET(CMAKE_INCLUDE_CURRENT_DIR ON)
##引入Qt库
#FIND_PACKAGE(Qt5Widgets REQUIRED)
#FIND_PACKAGE(Qt5Gui REQUIRED)
#FIND_PACKAGE(Qt5Core REQUIRED)
#FIND_PACKAGE(Qt5Sql REQUIRED)
#FIND_PACKAGE(Qt5Network REQUIRED)
#FIND_PACKAGE(Qt5Concurrent REQUIRED)
##添加预编译宏
#ADD_DEFINITIONS(-DTORRENT_LIBRARY)
#ADD_DEFINITIONS(-DNO_FREETYPE)
#ADD_DEFINITIONS(-DUNICODE -D_UNICODE)
#ADD_DEFINITIONS(-DHCPP_LEGACY_API)
##将各种文件归类到指定变量
#FILE(GLOB_RECURSE HEADER_FILES "*.h")
#FILE(GLOB_RECURSE SRC_FILES "*.cpp")
#FILE(GLOB_RECURSE FORMS "*.ui")
#FILE(GLOB_RECURSE RESOURCE_FILES "*.qrc")
#FILE(GLOB TS_FILES "*.ts")
#FILE(GLOB MOC_FILES "moc_*.cpp")
##将ui文件编译成ui_*.h文件
#IF (FORMS)
#    QT5_WRAP_UI(FORMS_UIC ${FORMS})
#ENDIF ()
##将包含Q_OBJECT的头文件编译成moc_*.cpp文件
#QT5_WRAP_CPP(MOC_FILES ${HEADER_FILES})
##启用qrc资源文件
#QT5_ADD_RESOURCES(RES_FILES resourse.qrc)
##启用当前头文件目录
#SET(CMAKE_INCLUDE_CURRENT_DIR ON)
##将ui文件和生成文件整理在一个文件夹中
#SOURCE_GROUP("Form Files" FILES ${FORMS})
##将qrc资源文件整理在一个文件夹中
#SOURCE_GROUP("Resource Files" FILES ${RESOURCE_FILES})
##查找当前目录下所有的.h和.cpp文件
#SOURCE_GROUP("Header Files" FILES ${HEADER_FILES})
#SOURCE_GROUP("Source Files" FILES ${SRC_FILES})
##翻译文件
#SOURCE_GROUP("Translation Files" FILES ${TS_FILES})
##将MOC,UI,QRC的中间生成文件编译进EXE中
#SOURCE_GROUP("Generated Files" FILES ${MOC_FILES} ${FORMS_UIC} ${RES_FILES} ${TS_FILES})
##引入库目录路径
##SET(SDK_PATH "../SDK-PATH")
##LINK_DIRECTORIES(${SDK_PATH}/Lib ${SDK_PATH}/opencv3.4/lib ${SDK_PATH}/libpng/lib ${SDK_PATH}/log4cplus/lib ${SDK_PATH}/zlib/lib)
##引入库目录路径
##LINK_DIRECTORIES(${CMAKE_BINARY_DIR}/x64)
##将所有文件编译成EXE,并设置以WIN32的方式运行
##ADD_EXECUTABLE(${PROJECT_NAME} WIN32 ${HEADER_FILES} ${SRC_FILES} ${MOC_FILES} ${FORMS_UIC} ${RESOURCE_FILES} ${RES_FILES})
##设置EXE文件的输出目录
##SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/x64)
##引入库目录头文件
#INCLUDE_DIRECTORIES(
#        ${SDK_PATH}/libpng/include
#        ${SDK_PATH}/zlib/include
#        ${SDK_PATH}/log4cplus/include
#        ${SDK_PATH}/opencv3.4/include
#        ${SDK_PATH}/opencv3.4/include/opencv
#        ${SDK_PATH}/opencv3.4/include/opencv2
#)
#INCLUDE_DIRECTORIES(${AUTOGEN_BUILD_DIR})
#INCLUDE_DIRECTORIES(../Define ../Algorithm)
##链接以上lib库
##TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${PROJECT_LIBRARIES})
###链接opencv开发库
##TARGET_LINK_LIBRARIES(${PROJECT_NAME}
##        debug opencv_world343d.liboptimized opencv_world343.lib
##        debug zlibstaticd.liboptimized zlibstatic.lib
##        debug libpng16_staticd.liboptimized libpng16_static.lib
##        debug log4cplusUD.liboptimized log4cplusU.lib
##        )
###加载静态LIB
###TARGET_LINK_LIBRARIES(${PROJECT_NAME}　Algorithm.lib)
##启用Qt的库模块
#TARGET_LINK_LIBRARIES(${PROJECT_NAME} Qt5::Widgets Qt5::Core Qt5::Gui Qt5::Sql Qt5::Network Qt5::Concurrent)
#QT5_USE_MODULES(${PROJECT_NAME} Widgets Core Gui Sql Network Concurrent)

