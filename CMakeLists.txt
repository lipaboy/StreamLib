cmake_minimum_required(VERSION 3.5)
project(Stream_Lib)


#------------Flags setting-------------#

    include(CheckCXXCompilerFlag)

    function(enable_cxx_compiler_flag_if_supported flag)
        string(FIND "${CMAKE_CXX_FLAGS}" "${flag}" flag_already_set)
        if(flag_already_set EQUAL -1)
            check_cxx_compiler_flag("${flag}" flag_supported)
            if(flag_supported)
                set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${flag}" PARENT_SCOPE)
            endif()
            unset(flag_supported CACHE)
        endif()
    endfunction()

    if (WIN32)
        enable_cxx_compiler_flag_if_supported("/std:c++17")
    else() # Linux
        enable_cxx_compiler_flag_if_supported("-std=c++17")
    endif()



#------------End Flags setting-------------#

# must be after compiler's flags checking
add_subdirectory(src)
add_subdirectory(tests)

#----------------START GTEST INCLUDING-----------------#

    include(CTest)

    if (CMAKE_VERSION VERSION_LESS 3.2)
        set(UPDATE_DISCONNECTED_IF_AVAILABLE "")
    else()
        set(UPDATE_DISCONNECTED_IF_AVAILABLE "UPDATE_DISCONNECTED 1")
    endif()

    include(DownloadProject.cmake)
    download_project(PROJ                googletest
                     GIT_REPOSITORY      https://github.com/google/googletest.git
                     GIT_TAG             main
                     ${UPDATE_DISCONNECTED_IF_AVAILABLE}
    )

    # Prevent GoogleTest from overriding our compiler/linker options
    # when building with Visual Studio
    set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

    add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR})

    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin/")

    # When using CMake 2.8.11 or later, header path dependencies
    # are automatically added to the gtest and gmock targets.
    # For earlier CMake versions, we have to explicitly add the
    # required directories to the header search path ourselves.
    if (CMAKE_VERSION VERSION_LESS 2.8.11)
        include_directories("${gtest_SOURCE_DIR}/include"
                            "${gmock_SOURCE_DIR}/include")
    endif()

#----------------END GTEST INCLUDING-----------------#

