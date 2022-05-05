# Almost all CMake files should start with this
# You should always specify a range with the newest
# and oldest tested versions of CMake. This will ensure
# you pick up the best policies.
cmake_minimum_required(VERSION 3.14)

# This is your project statement. You should always list languages;
# Listing the version is nice here since it sets lots of useful variables
project(
  gst-device-monitor
  VERSION 1.0
  LANGUAGES CXX)

# If you set any CMAKE_ variables, that can go here.
# (But usually don't do this, except maybe for C++ standard)

# Find packages go here.

include(cmake/detect_gstreamer.cmake)

if (HAVE_GSTREAMER)
	message ("    GStreamer: (${GSTREAMER_VERSION})")
else()
	message( FATAL_ERROR "GStreamer not found." )
endif()

# You should usually split this into folders, but this is a simple example


# Link each target with other targets or add options, etc.

# Adding something we can run - Output name matches target name
add_executable(gst-device-monitor main.cpp)

target_include_directories(gst-device-monitor PUBLIC
    ${GSTREAMER_INCLUDE_DIRS}
)

# Make sure you link your targets with this command. It can also link libraries and
# even flags, so linking a target that does not exist will not give a configure-time error.
target_link_libraries(gst-device-monitor PRIVATE ${GSTREAMER_LIBRARIES}
)
