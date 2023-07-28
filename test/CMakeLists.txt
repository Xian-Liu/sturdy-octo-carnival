set(DIR_TEST ${CMAKE_CURRENT_LIST_DIR}/test_first.cpp ${CMAKE_CURRENT_LIST_DIR}/test_main.cpp)
set(link_lib glog::glog GTest::gtest Threads::Threads)
set(link_math_lib ${ARMADILLO_LIBRARIES} BLAS::BLAS LAPACK::LAPACK)

add_executable(test_kuiper_course ${DIR_TEST})

include(GoogleTest)

target_link_libraries(test_kuiper_course ${link_lib} ${link_math_lib})

gtest_discover_tests(test_kuiper_course)
