
cmake_minimum_required(VERSION 3.12)
project(krglhwebp_krkrsdl2)

include(FetchContent)

FetchContent_Declare(
	krkrsdl2-tp_stub
	URL https://github.com/krkrsdl2/krkrsdl2/releases/download/latest/krkrsdl2-tp_stub.tar.gz
)

FetchContent_MakeAvailable(krkrsdl2-tp_stub)

set(KRGLHWEBP_SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR})
file(STRINGS ${KRGLHWEBP_SRC_DIR}/src_list/sources.txt KRGLHWEBP_SRC)
file(STRINGS ${KRGLHWEBP_SRC_DIR}/src_list/includes.txt KRGLHWEBP_INCLUDES)
list(TRANSFORM KRGLHWEBP_SRC PREPEND ${KRGLHWEBP_SRC_DIR}/)
list(TRANSFORM KRGLHWEBP_INCLUDES PREPEND ${KRGLHWEBP_SRC_DIR}/)

add_library(krglhwebp MODULE)
set_target_properties(krglhwebp PROPERTIES CXX_STANDARD 11)
set_target_properties(krglhwebp PROPERTIES PREFIX "")
target_sources(krglhwebp PRIVATE ${KRGLHWEBP_SRC})
target_include_directories(krglhwebp PRIVATE ${KRGLHWEBP_INCLUDES})
target_link_libraries(krglhwebp tp_stub)
