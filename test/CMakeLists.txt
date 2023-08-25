set(DIR_TEST 
    ${CMAKE_CURRENT_LIST_DIR}/test_tensor.cpp
    ${CMAKE_CURRENT_LIST_DIR}/test_first.cpp
    ${CMAKE_CURRENT_LIST_DIR}/test_load_data.cpp
    ${CMAKE_CURRENT_LIST_DIR}/test_relu.cpp
    ${CMAKE_CURRENT_LIST_DIR}/test_main.cpp
)

set(link_lib glog::glog GTest::gtest Threads::Threads)
set(link_math_lib ${ARMADILLO_LIBRARIES} BLAS::BLAS LAPACK::LAPACK)

add_executable(test_kuiper_course ${DIR_TEST})

target_link_libraries(test_kuiper_course 
    ${link_lib} 
    ${link_math_lib} 
    kuiper_tensor
)

target_include_directories(test_kuiper_course 
    PRIVATE ${PROJECT_SOURCE_DIR}/include
)

gtest_discover_tests(test_kuiper_course)
