cmake_minimum_required(VERSION 3.16)
project(kuiper_course)

set(CMAKE_CXX_STANDARD 17)

find_package(glog REQUIRED)
find_package(GTest REQUIRED)
find_package(Threads REQUIRED)
find_package(BLAS REQUIRED)
find_package(LAPACK REQUIRED)
find_package(Armadillo REQUIRED)
set(link_lib glog::glog GTest::gtest Threads::Threads)
set(link_math_lib ${ARMADILLO_LIBRARIES} BLAS::BLAS LAPACK::LAPACK)
add_executable(kuiper_course main.cpp)

add_library(kuiper_tensor OBJECT 
    ${PROJECT_SOURCE_DIR}/source/data/tensor.cpp
    ${PROJECT_SOURCE_DIR}/source/data/load_data.cpp
    ${PROJECT_SOURCE_DIR}/source/factory/layer_factory.cpp
    ${PROJECT_SOURCE_DIR}/source/layer/layer.cpp
    ${PROJECT_SOURCE_DIR}/source/layer/relu_layer.cpp
    ${PROJECT_SOURCE_DIR}/source/ops/op.cpp
    ${PROJECT_SOURCE_DIR}/source/ops/relu_op.cpp
)

target_include_directories(
    kuiper_tensor
    PUBLIC
        ${ARMADILLO_INCLUDE_DIRS} 
        ${PROJECT_SOURCE_DIR}/include
)

target_include_directories(
    kuiper_course 
    PUBLIC 
        ${ARMADILLO_INCLUDE_DIRS} 
        ${PROJECT_SOURCE_DIR}/include
)
target_link_libraries(kuiper_course ${link_lib} ${link_math_lib})

enable_testing()

add_subdirectory(test)
