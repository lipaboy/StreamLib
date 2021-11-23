#cmake_minimum_required(VERSION 2.8.2)
project(Lipaboy_Library_Source)

set(LIB_LIPABOY_LIB_SOURCE_FILES

    # Extra tools
    extra_tools/extra_tools.h
    extra_tools/initializer_list_iterator.h
    extra_tools/maths_tools.h
    extra_tools/producing_iterator.h
    extra_tools/sequence_producing_iterator.h
    extra_tools/detect_time_duration.h

    # Stream
    stream/stream_extended.h
    "stream/stream_base.h"
    stream/stream.h
    stream/light_stream.h
    
    # Operators
    stream/operators/tupled.h
    "stream/operators/to_pair.h"
    stream/operators/distinct.h
    "stream/operators/filter.h"
    "stream/operators/get.h"
    stream/operators/group_by_vector.h
    stream/operators/map.h
    stream/operators/nth.h
    stream/operators/operators.h
    stream/operators/print_to.h
    stream/operators/reduce.h
    stream/operators/skip.h
    stream/operators/sum.h
    stream/operators/to_vector.h
    stream/operators/tools.h
    stream/operators/ungroup_by_bit.h
    stream/operators/split.h
    stream/operators/min.h
    stream/operators/max.h
    stream/operators/cast.h

    # Short Stream
    stream/short_stream/stream_base.h
    stream/short_stream/stream_extended.h
    stream/short_stream/stream.h
    "stream/short_stream/operators/filter.h"
    stream/short_stream/operators/tools.h 
    "stream/short_stream/operators/get.h"
    stream/short_stream/operators/sum.h
    stream/short_stream/operators/operators.h

    # Fast Stream
    stream/fast_stream/stream_base.h
    stream/fast_stream/stream_extended.h
    stream/fast_stream/stream.h
    "stream/fast_stream/operators/filter.h"
    "stream/fast_stream/operators/get.h"
    stream/fast_stream/operators/sum.h
    stream/fast_stream/operators/skip.h
    stream/fast_stream/operators/tools.h
    stream/fast_stream/operators/operators.h

)

# Declare the library
add_library(LIPABOY_LIB INTERFACE ${LIB_LIPABOY_LIB_SOURCE_FILES})


find_package(OpenMP)
    if (OPENMP_FOUND)
        set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
        set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    endif()

	# BOOST library connection

#if(WIN32)
#	add_definitions( -DBOOST_ALL_DYN_LINK )  #If not VS will give linking errors of redefinitions
#	set(Boost_USE_STATIC_LIBS OFF )
#	set(Boost_USE_MULTITHREADED ON)
#	set(Boost_USE_STATIC_RUNTIME OFF)
#    find_package(Boost COMPONENTS thread chrono regex REQUIRED )
#
#    INCLUDE_DIRECTORIES(${Boost_INCLUDE_DIRS})
#endif(WIN32)

#if(WIN32)
#    TARGET_LINK_LIBRARIES( LIPABOY_LIB ${Boost_LIBRARIES} )
#endif(WIN32)


# Specify here the include directories exported
# by this library
target_include_directories(LIPABOY_LIB INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}
)

set_directory_properties(PROPERTIES COMPILE_DEFINITIONS_DEBUG "_DEBUG")


