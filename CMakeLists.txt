cmake_minimum_required(VERSION 2.8)

project(png)

find_package(ZLIB)
if (NOT ZLIB_FOUND)
	message(STATUS "ZLib not found.")
	set(CPM_DIR "${CMAKE_CURRENT_BINARY_DIR}/cpm_packages" CACHE TYPE STRING)
	find_package(Git)
	if(NOT GIT_FOUND)
		message(FATAL_ERROR "CPM requires Git.")
	endif()
	if (NOT EXISTS ${CPM_DIR}/CPM.cmake)
		message(STATUS "Cloning repo (https://github.com/iauns/cpm)")
		execute_process(
				COMMAND "${GIT_EXECUTABLE}" clone https://github.com/iauns/cpm ${CPM_DIR}
				RESULT_VARIABLE error_code
				OUTPUT_QUIET ERROR_QUIET)
		if(error_code)
			message(FATAL_ERROR "CPM failed to get the hash for HEAD")
		endif()
	endif()
	include(${CPM_DIR}/CPM.cmake)

	CPM_AddModule("zlib"
			GIT_REPOSITORY "https://github.com/rinthel/cpm-zlib")
	CPM_Finish()
endif()


file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/scripts/pnglibconf.h.prebuilt DESTINATION ${CMAKE_CURRENT_SOURCE_DIR})
file(RENAME ${CMAKE_CURRENT_SOURCE_DIR}/pnglibconf.h.prebuilt ${CMAKE_CURRENT_SOURCE_DIR}/pnglibconf.h)

set(SOURCE_FILES
	png.c
	png.h
	pngconf.h
	pngdebug.h
	pngerror.c
	pngget.c
	pnginfo.h
	pngmem.c
	pngpread.c
	pngpriv.h
	pngread.c
	pngrio.c
	pngrtran.c
	pngrutil.c
	pngset.c
	pngstruct.h
	pngtrans.c
	pngwio.c
	pngwrite.c
	pngwtran.c
	pngwutil.c
	arm/filter_neon_intrinsics.c
	arm/arm_init.c
	)

add_library(png ${SOURCE_FILES})
