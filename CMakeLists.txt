cmake_minimum_required(VERSION 3.8)
project(gginput VERSION 1.0)

option(build_example "build examples?" ON)
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

file(GLOB SOURCES src/*.cc)
file(GLOB HEADERS src/*.h)

add_library(${PROJECT_NAME} SHARED ${SOURCES})

install (TARGETS ${PROJECT_NAME}  
	RUNTIME DESTINATION bin
	ARCHIVE DESTINATION lib
	LIBRARY DESTINATION lib
)
install(FILES ${HEADERS} DESTINATION include/${PROJECT_NAME})

target_include_directories(
    ${PROJECT_NAME} 
    PUBLIC  
        deps/gainput/lib/include
)
target_link_libraries(
    ${PROJECT_NAME} 
	PUBLIC
)
target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_11)

if(WIN32)
	target_link_libraries(
		${PROJECT_NAME} 
	)
endif(WIN32)

if(APPLE)
endif(APPLE)

if(build_example)
	add_subdirectory(example)
endif(build_example)