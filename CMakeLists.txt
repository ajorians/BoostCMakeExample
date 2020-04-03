CMAKE_MINIMUM_REQUIRED(VERSION 3.10)

PROJECT(TestMe)

FILE(GLOB SOURCE_FILES "main.cpp")

SOURCE_GROUP(Source FILES ${SOURCE_FILES})

IF( MSVC )
set(Boost_USE_STATIC_LIBS   ON)
ELSE()
set(Boost_USE_STATIC_LIBS   OFF)
ENDIF()
find_package(Boost COMPONENTS date_time REQUIRED)
set(CMAKE_CXX_STANDARD 17)

add_executable( Test ${SOURCE_FILES} )

target_link_libraries(Test Boost::date_time)

# Use Unicode Character set
target_compile_definitions(Test PUBLIC UNICODE )
target_compile_definitions(Test PUBLIC _UNICODE )

