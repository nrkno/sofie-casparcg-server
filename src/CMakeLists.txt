cmake_minimum_required (VERSION 3.16)

# Project settings
PROJECT ("CasparCG Server")
SET (CONFIG_VERSION_MAJOR 2)
SET (CONFIG_VERSION_MINOR 4)
SET (CONFIG_VERSION_BUG 0)
SET (CONFIG_VERSION_TAG "NRK-Dev")

option(ENABLE_HTML "Enable HTML module, require CEF" ON)

# Add custom cmake modules path
SET (CASPARCG_PATCH_DIR ${CMAKE_SOURCE_DIR}/CMakeModules/patches)
LIST (APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/CMakeModules)

if (MSVC)
	INCLUDE (Bootstrap_Windows)
else ()
	INCLUDE (Bootstrap_Linux)

	# Output build settings
	MESSAGE (STATUS "Target platform: ${CONFIG_PLATFORM}")
	MESSAGE (STATUS "Target architecture: ${CONFIG_ARCH}")
	MESSAGE (STATUS "CPU Count: ${CONFIG_CPU_COUNT}")
	MESSAGE (STATUS "Target build type: ${CMAKE_BUILD_TYPE}")
	MESSAGE (STATUS "Build Version: ${CONFIG_VERSION_MAJOR}.${CONFIG_VERSION_MINOR}.${CONFIG_VERSION_BUG} ${CONFIG_VERSION_TAG} (Revision: ${CONFIG_VERSION_GIT_HASH})")

	CONFIGURE_FILE ("${PROJECT_SOURCE_DIR}/version.tmpl" "${CMAKE_BINARY_DIR}/generated/version.h")
	INCLUDE_DIRECTORIES ("${CMAKE_BINARY_DIR}/generated")

	ADD_SUBDIRECTORY (tools)
	ADD_SUBDIRECTORY (accelerator)
	ADD_SUBDIRECTORY (common)
	ADD_SUBDIRECTORY (core)
	ADD_SUBDIRECTORY (modules)
	ADD_SUBDIRECTORY (protocol)
	ADD_SUBDIRECTORY (shell)
endif ()
