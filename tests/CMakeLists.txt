set(MODULE_NAME Stream_Lib)

include_directories("${CMAKE_SOURCE_DIR}/tests")
include_directories("${CMAKE_SOURCE_DIR}/src")

set(TEST_SOURCE
    tests.cpp

	# Stream
    stream/stream_tests.cpp
    stream/stream_test.h
    stream/benchmarks/stream_vs_fast_stream.cpp

    stream/tupled_stream_tests.cpp
    stream/paired_stream_tests.cpp
    stream/nop_tests.cpp
    stream/nth_tests.cpp
    stream/filter_tests.cpp
    stream/reduce_tests.cpp
    stream/max_min_tests.cpp
    stream/split_tests.cpp
    stream/cast_tests.cpp

	# Extra tools
    extra_tools/producing_iterator_tests.cpp
    extra_tools/initializer_list_iterator_tests.cpp
    extra_tools/extra_tools_tests.cpp
    extra_tools/extra_tools_tests.h
)

add_executable(${MODULE_NAME}_tests ${TEST_SOURCE})

target_link_libraries(${MODULE_NAME}_tests 
	STREAM_LIB 
	gtest 
    gmock_main)

add_test(NAME ${MODULE_NAME}_tests COMMAND ${MODULE_NAME}_tests)

set_directory_properties(PROPERTIES COMPILE_DEFINITIONS_DEBUG "_DEBUG")