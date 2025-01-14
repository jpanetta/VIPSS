project(vipss)
cmake_minimum_required(VERSION 2.8)

if(NOT CMAKE_BUILD_TYPE)
    message(STATUS "No build type selected, default to Release")
    set(CMAKE_BUILD_TYPE "Release")
endif()

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

find_package(NLopt REQUIRED)
set(NLOPT_LIB_DIR "")
set(NLOPT_LIB ${NLOPT_LIBRARIES})

find_package(Armadillo REQUIRED)
set(ARMADILLO_LIB_DIRS "")
set(ARMADILLO_LIB ${ARMADILLO_LIBRARIES})

include_directories(${NLOPT_INCLUDE_DIRS} ${ARMADILLO_INCLUDE_DIRS} ./src/surfacer)
aux_source_directory(. MAIN)
aux_source_directory(./src SRC_LIST)
aux_source_directory(./src/surfacer SURFACER_LIST)

LINK_DIRECTORIES(${ARMADILLO_LIB_DIRS} ${NLOPT_LIB_DIR})
add_executable(${PROJECT_NAME} ${SRC_LIST} ${MAIN} ${SURFACER_LIST})

target_link_libraries(${PROJECT_NAME} ${ARMADILLO_LIB} ${NLOPT_LIB})

set_target_properties(${PROJECT_NAME} PROPERTIES CXX_STANDARD 11)
set_target_properties(${PROJECT_NAME} PROPERTIES CXX_STANDARD_REQUIRED ON)
