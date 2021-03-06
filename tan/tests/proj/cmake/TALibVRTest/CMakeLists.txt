cmake_minimum_required(VERSION 3.10)

# The cmake-policies(7) manual explains that the OLD behaviors of all
# policies are deprecated and that a policy should be set to OLD only under
# specific short-term circumstances.  Projects should be ported to the NEW
# behavior and not rely on setting a policy to OLD.

# VERSION not allowed unless CMP0048 is set to NEW
if (POLICY CMP0048)
  cmake_policy(SET CMP0048 NEW)
endif (POLICY CMP0048)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_SKIP_RULE_DEPENDENCY TRUE)

enable_language(CXX)

include(../../../../tanlibrary/proj/cmake/utils/OpenCL.cmake)

# name
project(TALibVRTest DESCRIPTION "TALibVRTest")

include_directories(../../../../../amf)
include_directories(../../../../../tan)

include_directories(../../../../common)

ADD_DEFINITIONS(-D_CONSOLE)
ADD_DEFINITIONS(-D_LIB)
ADD_DEFINITIONS(-DUNICODE)
ADD_DEFINITIONS(-D_UNICODE)

if(IS_DIRECTORY ${IPP_DIR})
# enable IPP
 link_directories(${IPP_DIR}/lib/intel64_win)
endif()

# sources
set(
  SOURCE_EXE
  ../../../../common/wav.cpp
  ../../../../common/FileUtility.cpp

  ../../../src/TALibVRTest/stdafx.cpp
  ../../../src/TALibVRTest/TALibVRTest.cpp
  )

set(
  HEADER_EXE
  ../../../../common/wav.h
  ../../../../common/FileUtility.h

  ../../../src/TALibVRTest/stdafx.h
  ../../../src/TALibVRTest/targetver.h
  )

# create binary
add_executable(
  TALibVRTest
  ${SOURCE_EXE}
  ${HEADER_EXE}
  )

  target_link_libraries(TALibVRTest TrueAudioNext)
  target_link_libraries(TALibVRTest GPUUtilities)
  target_link_libraries(TALibVRTest TrueAudioVR)