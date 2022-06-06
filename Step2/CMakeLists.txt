cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# If you'd like to build in a Unix way in windows platform,
# add the following
SET(MY_MINGW64_HOME "D:/procs/mingw64")
SET(CMAKE_MAKE_PROGRAM "${MY_MINGW64_HOME}/bin/mingw32-make.exe")
SET(CMAKE_C_COMPILER "${MY_MINGW64_HOME}/bin/gcc.exe")
SET(CMAKE_CXX_COMPILER "${MY_MINGW64_HOME}/bin/g++.exe")

option(USE_MYMATH "Use tutorial provided math implementation" ON)

if(USE_MYMATH)
	# Add the MathFunctions library
	add_subdirectory(MathFunctions)
	list(APPEND EXTRA_LIBS MathFunctions)
	list(APPEND EXTRA_INCLUDES "${PROJECT_SOURCE_DIR}/MathFunctions")
endif()

# configure a header file to pass some of the CMake settings
# to the source code
configure_file(TutorialConfig.h.in TutorialConfig.h)

# add the executable
add_executable(Tutorial tutorial.cxx MathFunctions/mysqrt.cxx)

target_link_directories(Tutorial PUBLIC ${EXTRA_LIBS})

# add the binary tree to the search path for include files
# so that we will find TutorialConfig.h
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           "${EXTRA_INCLUDES}"
                           )



