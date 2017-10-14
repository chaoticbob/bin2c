cmake_minimum_required(VERSION 2.8)

project(bin2c)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")

if(WIN32)
  list(APPEND GETOPT_FILES getopt/getopt.h getopt/getopt.c)
endif()

add_executable(bin2c
               bin2c/main.c
               ${GETOPT_FILES})

target_include_directories(bin2c PRIVATE ${CMAKE_SOURCE_DIR}/getopt)

if(WIN32)
    set_target_properties(bin2c PROPERTIES LINK_FLAGS "/ENTRY:mainCRTStartup /SUBSYSTEM:Windows /INCREMENTAL:NO")
    target_compile_definitions(bin2c PRIVATE _CRT_SECURE_NO_WARNINGS)
endif()

install(TARGETS bin2c RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX})
