# - Top level CMake script for TextInput
# Require CMake 2.8.8 at minimum to allow support of OBJECT libs in
# future
cmake_minimum_required(VERSION 2.8.8)
project(TextInput)

#-----------------------------------------------------------------------
# Configuration
include_directories(${PROJECT_SOURCE_DIR})

#-----------------------------------------------------------------------
# Build library
#
set(TextInput_PUBLIC_HDRS
  textinput/Callbacks.h
  textinput/Color.h
  textinput/Display.h
  textinput/Editor.h
  textinput/History.h
  textinput/InputData.h
  textinput/KeyBinding.h
  textinput/Range.h
  textinput/Reader.h
  textinput/SignalHandler.h
  textinput/StreamReader.h
  textinput/TerminalDisplay.h
  textinput/Text.h
  textinput/TextInputContext.h
  textinput/TextInput.h
  )

set(TextInput_PUBLIC_SRCS
  textinput/Editor.cpp
  textinput/History.cpp
  textinput/KeyBinding.cpp
  textinput/Range.cpp
  textinput/SignalHandler.cpp
  textinput/StreamReader.cpp
  textinput/TerminalDisplay.cpp
  textinput/TextInputContext.cpp
  textinput/TextInput.cpp
  )

if(UNIX)
  set(TextInput_PRIVATE_SRCS
    textinput/StreamReaderUnix.h
    textinput/TerminalConfigUnix.h
    textinput/TerminalDisplayUnix.h
    textinput/StreamReaderUnix.cpp
    textinput/TerminalConfigUnix.cpp
    textinput/TerminalDisplayUnix.cpp
    )
elseif(WIN32)
  set(TextInput_PRIVATE_SRCS
    textinput/StreamReaderWin.h
    textinput/TerminalDisplayWin.h
    textinput/StreamReaderWin.cpp
    textinput/TerminalDisplayWin.cpp
    )
endif()

add_library(TextInput ${TextInput_PUBLIC_HDRS} ${TextInput_PUBLIC_SRCS} ${TextInput_PRIVATE_SRCS})

