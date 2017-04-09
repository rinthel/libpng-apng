cmake_minimum_required(VERSION 2.8)

project(png)

file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/scripts/pnglibconf.h.prebuilt DESTINATION ${CMAKE_CURRENT_SOURCE_DIR})
file(RENAME ${CMAKE_CURRENT_SOURCE_DIR}/pnglibconf.h.prebuilt ${CMAKE_CURRENT_SOURCE_DIR}/pnglibconf.h)

set(HEADERS
	png.h
	pngconf.h
	pnglibconf.h
	)
set(SOURCE_FILES
	png.c
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

add_library(png ${SOURCE_FILES} ${HEADERS})

install(TARGETS png DESTINATION lib)
install(FILES ${HEADERS} DESTINATION include)