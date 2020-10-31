CMAKE_MINIMUM_REQUIRED(VERSION 3.10)

PROJECT(TestMe 
	VERSION 1.0 
	DESCRIPTION "Test Project" 
	LANGUAGES CXX C)

################
# Dependencies #
################

# Download automatically, you can also just copy the conan.cmake file
if(NOT EXISTS "${CMAKE_BINARY_DIR}/conan.cmake")
   message(STATUS "Downloading conan.cmake from https://github.com/conan-io/cmake-conan")
   file(DOWNLOAD "https://github.com/conan-io/cmake-conan/raw/v0.15/conan.cmake"
                 "${CMAKE_BINARY_DIR}/conan.cmake" 
                 TLS_VERIFY ON)
endif()

include(${CMAKE_BINARY_DIR}/conan.cmake)
conan_cmake_run(REQUIRES 
   boost/1.73.0
   gtest/1.10.0
   BASIC_SETUP
   BUILD missing)

FILE(GLOB SOURCE_FILES "main.cpp")

SOURCE_GROUP(Source FILES ${SOURCE_FILES})

add_executable( Test ${SOURCE_FILES} )

target_link_libraries(Test ${CONAN_LIBS})

