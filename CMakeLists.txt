project(dspfilter )
cmake_minimum_required(VERSION 3.13)

set(CMAKE_VERBOSE_MAKEFILE on)
set(CMAKE_CXX_COMPILER $ENV{CXX})
set(CMAKE_CXX_FLAGS "-O3 -std=c++11 ")

link_directories(lib)

SET(SRC_MOUDLE
    src/AudioFileReader.h
    src/AudioFileReader.cpp
    src/Clipper.h
    src/Clipper.cpp
    src/CubeClipper.h
    src/CubeClipper.cpp
    src/Processor.h
    src/Processor.cpp
    src/SndFileReader.h
    src/SndFileReader.cpp
    src/TanhClipper.h
    src/TanhClipper.cpp
)

set(SRC_LIST
	src/Main.cpp
	${SRC_MOUDLE}
)

set(LINK_LIBRARIES sndfile)

add_executable(dspfilter ${SRC_LIST})
target_link_libraries(dspfilter ${LINK_LIBRARIES})
set_target_properties(dspfilter PROPERTIES LINKER_LANGUAGE CXX)


enable_testing()

include_directories(src)
link_directories(lib src)

set(TESTS
	test/SndFileReader.t.cpp
    test/CubeClipper.t.cpp
	test/DspFilter.m.t.cpp)

set(TEST_LINK_LIBRARIES gtest)

add_executable(dspfilter_tests ${TESTS} ${SRC_MOUDLE})

target_link_libraries(dspfilter_tests ${LINK_LIBRARIES} ${TEST_LINK_LIBRARIES})

add_test(dspfilter_tests dspfilter_tests)
