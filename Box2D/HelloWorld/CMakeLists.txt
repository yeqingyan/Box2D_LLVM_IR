# Hello World examples
set(CMAKE_VERBOSE_MAKEFILE ON)
include_directories (${Box2D_SOURCE_DIR})

add_custom_command(OUTPUT HelloWorld.ll
                COMMAND ${CMAKE_CXX_COMPILER} -fno-use-cxa-atexit -S -emit-llvm -I${CMAKE_SOURCE_DIR} -c ${CMAKE_SOURCE_DIR}/HelloWorld/HelloWorld.cpp
 				COMMAND llvm-link -S ../Box2D/Box2DLL.ll HelloWorld.ll  -o HelloWorld_main.ll
                DEPENDS ${CMAKE_BINARY_DIR}/Box2D/Box2DLL.ll ${CMAKE_SOURCE_DIR}/HelloWorld/HelloWorld.cpp)

add_custom_target(HelloWorld DEPENDS Box2D HelloWorld.ll)

add_custom_command(OUTPUT Bench2d.ll
                COMMAND ${CMAKE_CXX_COMPILER} -fno-use-cxa-atexit -S -emit-llvm -I${CMAKE_SOURCE_DIR} -c ${CMAKE_SOURCE_DIR}/HelloWorld/Bench2d.cpp
 				COMMAND llvm-link -S ../Box2D/Box2DLL.ll Bench2d.ll  -o Bench2D_main.ll
                DEPENDS ${CMAKE_BINARY_DIR}/Box2D/Box2DLL.ll ${CMAKE_SOURCE_DIR}/HelloWorld/Bench2d.cpp)

add_custom_target(BENCH2D DEPENDS Box2D Bench2d.ll)
# add_executable(HelloWorld HelloWorld.cpp)
# target_link_libraries (HelloWorld Box2D)
