cmake_minimum_required(VERSION 3.20)

file(GLOB_RECURSE PSYCROSS_SRCS_C
	"*.c" "*.C"
)

file(GLOB_RECURSE PSYCROSS_SRCS_CPP
	"*.cpp"
)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-narrowing")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-narrowing")

set_source_files_properties( ${PSYCROSS_SRCS_C} PROPERTIES LANGUAGE C)
set_source_files_properties( ${PSYCROSS_SRCS_CPP} PROPERTIES LANGUAGE CXX)
#set_source_files_properties( "src/gte/PsyX_GTE.cpp" PROPERTIES LANGUAGE C)

add_library(psycross_static STATIC ${PSYCROSS_SRCS_C} ${PSYCROSS_SRCS_CPP})
set_target_properties(psycross_static PROPERTIES OUTPUT_NAME "psycross")
target_include_directories(psycross_static PUBLIC "include" "include/psx")

find_package(SDL2 REQUIRED)
target_link_libraries(psycross_static ${SDL2_LIBRARIES})
target_include_directories(psycross_static PRIVATE ${SDL2_INCLUDE_DIRS})

find_package(OpenAL REQUIRED)
target_link_libraries(psycross_static OpenAL)
target_include_directories(psycross_static PRIVATE ${OpenAL_BINARY_DIR} ${OpenAL_SOURCE_DIR}/include)