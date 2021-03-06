cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(solver_cpp)

set(PRINT_VERSION_MAJOR 0)
set(PRINT_VERSION_MINOR 1)
set(PRINT_VERSION_PATCH 0)
set(PRINT_VERSION_TWEAK 0)
set(PRINT_VERSION ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
set(PRINT_VERSION_STRING "v${PRINT_VERSION}")

add_executable(solver ${CMAKE_CURRENT_SOURCE_DIR}/solver_application/equation.cpp)

add_library(solver_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib/solver.cpp)	

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex_lib)

target_include_directories(solver PUBLIC
	${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib/
	${CMAKE_CURRENT_SOURCE_DIR}/solver_lib/
)

target_link_libraries(solver solver_lib formatter_ex_lib)

install(TARGETS solver
	RUNTIME DESTINATION bin)

include(CPackConfig.cmake)
