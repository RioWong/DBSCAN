cmake_minimum_required(VERSION 2.8)

SET(CMAKE_C_FLAGS "-std=gnu99 -fPIC -fopenmp -mtune=corei7-avx")
SET(CMAKE_CXX_FLAGS "-std=c++0x -Wall -fPIC -fopenmp -mtune=corei7-avx")

set(Boost_USE_STATIC_LIBS OFF)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_RUNTIME OFF)

find_package(Boost 1.54.0 COMPONENTS timer system)

add_definitions(-DBOOST_UBLAS_NDEBUG)

if(Boost_FOUND)
    add_library(dbscan dbscan.cpp)

    add_executable(test_dbscan test_dbscan.cpp)
    target_link_libraries(test_dbscan dbscan ${Boost_LIBRARIES} pHash)
endif()
