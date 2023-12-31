# requires minimum cmake version
cmake_minimum_required(VERSION 3.12)

# produce the cmake var PROJECT_NAME
project(tutorial_yarp-basics)

# mandatory use of these packages
find_package(ICUBcontrib REQUIRED)
find_package(YARP 3.4.0 REQUIRED os dev sig cv)
find_package(OpenCV REQUIRED)

# extend the current search path used by cmake to load helpers
list(APPEND CMAKE_MODULE_PATH ${ICUBCONTRIB_MODULE_PATH})

# helpers defining certain macros
include(ICUBcontribHelpers)
include(ICUBcontribOptions)

# specify to install in $ICUBcontrib_DIR/bin
icubcontrib_set_default_prefix()

# building module
include_directories(${CMAKE_SOURCE_DIR}/src)

# buulding server
add_executable(${PROJECT_NAME} src/main.cpp src/TutorialModule.h src/TutorialModule.cpp)
target_link_libraries(${PROJECT_NAME} ${YARP_LIBRARIES} ${OpenCV_LIBS})
install(TARGETS ${PROJECT_NAME} DESTINATION bin)

# generate ad-hoc project to perform "make uninstall"
icubcontrib_add_uninstall_target()

file(GLOB resources ${CMAKE_SOURCE_DIR}/resources/*)
yarp_install(FILES ${resources} DESTINATION ${ICUBCONTRIB_CONTEXTS_INSTALL_DIR}/${PROJECT_NAME})
