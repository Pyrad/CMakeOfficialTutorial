# Set the minimun version of CMake
CMAKE_MINIMUM_REQUIRED(VERSION 3.10)

# Set the project name
PROJECT(Tutorial VERSION 1.0)

# specify the C++ standard
SET(CMAKE_CXX_STANDARD 11)
SET(CMAKE_CXX_STANDARD_REQUIRED True)

# Add the executable
ADD_EXECUTABLE(Tutorial tutorial.cxx)

# If you'd like to build in a Unix way in windows platform,
# add the following
SET(MY_MINGW64_HOME "D:/procs/mingw64")
SET(CMAKE_MAKE_PROGRAM "${MY_MINGW64_HOME}/bin/mingw32-make.exe")
SET(CMAKE_C_COMPILER "${MY_MINGW64_HOME}/bin/gcc.exe")
SET(CMAKE_CXX_COMPILER "${MY_MINGW64_HOME}/bin/g++.exe")


CONFIGURE_FILE(TutorialConfig.h.in TutorialConfig.h)


TARGET_INCLUDE_DIRECTORIES(Tutorial PUBLIC "${PROJECT_BINARY_DIR}" )

