project(factorial)

# Build factorial as library
add_library(factorial factorial.cpp)

include(FetchContent)
FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)

set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

# Find gtest
enable_testing()

# Find POSIX threads for UNIX
find_package(Threads REQUIRED)

# Build test
add_executable(factorialTest factorialTest.cpp)
target_link_libraries(factorialTest factorial 
    GTest::gtest_main
    GTest::gmock_main
    Threads::Threads
)

include(GoogleTest)
gtest_discover_tests(factorialTest)