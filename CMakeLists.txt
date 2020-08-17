cmake_minimum_required (VERSION 2.8)
set(TARGET_NAME "ChessCards")
project(${TARGET_NAME})

include_directories(${PROJECT_SOURCE_DIR})

#自定义的lib工程
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror -Wextra -Wpointer-arith -Wcast-qual -Wunreachable-code -Wredundant-decls -g -pipe -fPIC -std=c++11")

aux_source_directory(./majong SRC)
aux_source_directory(./poker SRC2)
aux_source_directory(./zipai SRC3)

list(APPEND TARGET_SRC ${SRC} ${SRC2} ${SRC3})

if(WIN32)
	file(GLOB HEAD ./majong/*.h*)
	file(GLOB HEAD2 ./poker/*.h*)
	file(GLOB HEAD3 ./zipai/*.h)
	list(APPEND TARGET_HDR ${HEAD} ${HEAD2} ${HEAD3})

    add_library(${TARGET_NAME} ${TARGET_SRC} ${TARGET_HDR})
	source_group("majong" FILES ${HEAD} ${SRC})
	source_group("poker" FILES ${HEAD2} ${SRC2})
	source_group("zipai" FILES ${HEAD3} ${SRC3})
else(WIN32)
	SET_CCACHE_COMPLER()
    add_library(${TARGET_NAME} SHARED ${TARGET_SRC})
endif(WIN32)
