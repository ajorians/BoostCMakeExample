CMAKE_MINIMUM_REQUIRED(VERSION 3.10)

PROJECT(TestMe)

FILE(GLOB SOURCE_FILES "main.cpp")

SOURCE_GROUP(Source FILES ${SOURCE_FILES})

add_executable( Test ${SOURCE_FILES} )

set( Boost_USE_STATIC_LIBS OFF )
set( Boost_USE_MULTITHREADED ON )
# Boost is suppose to add through pragma the libraries it wants to link with.  I was having trouble on MSVC
IF( MSVC )
   add_compile_definitions(BOOST_ALL_NO_LIB)
   target_link_libraries( Test bcrypt.lib )
   find_package( Boost REQUIRED COMPONENTS date_time filesystem thread system)
   target_include_directories( Test PUBLIC ${Boost_INCLUDE_DIRS} )
   target_link_libraries( Test ${Boost_DATE_TIME_LIBRARY} ${Boost_FILESYSTEM_LIBRARY} ${Boost_THREAD_LIBRARY} ${Boost_SYSTEM_LIBRARY})
ELSE()
   find_package( Boost COMPONENTS date_time REQUIRED)
   target_include_directories( Test PUBLIC ${Boost_INCLUDE_DIRS} )
   LINK_DIRECTORIES( ${Boost_LIBRARY_DIRS})
   TARGET_LINK_LIBRARIES( Test ${Boost_LIBRARIES})
ENDIF()

# Use C++Latest
set_property(TARGET Test PROPERTY CXX_STANDARD 17)

# Use Unicode Character set
target_compile_definitions(Test PUBLIC UNICODE )
target_compile_definitions(Test PUBLIC _UNICODE )

