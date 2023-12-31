cmake_minimum_required(VERSION 3.1...3.27)

project(
  RingFifoCTestProj
  VERSION 1.0
  LANGUAGES C CXX)


include(FetchContent)
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG "origin/main"
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

add_executable(RingFifoCTest)
target_sources(RingFifoCTest PUBLIC 
  fifo_test.cpp
)

target_include_directories(RingFifoCTest PUBLIC ./ ../../ring_fifo_c/)
target_link_libraries(RingFifoCTest PUBLIC RingFifoC PRIVATE GTest::gtest_main)
target_compile_features(RingFifoCTest PUBLIC cxx_std_20)

include(GoogleTest)
gtest_discover_tests(RingFifoCTest)
