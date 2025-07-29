# CMakeLists.txt in project_root/tests/
cmake_minimum_required(VERSION 3.10)
project(DroneDQN_Tests LANGUAGES CXX)

# Find Catch2 (assuming it's a submodule or installed)
find_package(Catch2 QUIET)
if (NOT Catch2_FOUND)
    # If Catch2 is a submodule in lib/Catch2
    add_subdirectory(${CMAKE_SOURCE_DIR}/lib/Catch2 Catch2)
endif()

# Test sources
set(TEST_SOURCES
    test_environment.cpp
    test_neural_network.cpp
    test_replay_buffer.cpp
    test_dqn_agent.cpp
    test_utils.cpp
    ${CMAKE_SOURCE_DIR}/src/environment.cpp
    ${CMAKE_SOURCE_DIR}/src/neural_network.cpp
    ${CMAKE_SOURCE_DIR}/src/replay_buffer.cpp
    ${CMAKE_SOURCE_DIR}/src/dqn_agent.cpp
    ${CMAKE_SOURCE_DIR}/src/utils.cpp
)

# Create test executable
add_executable(tests ${TEST_SOURCES})

# Include directories
target_include_directories(tests PRIVATE ${CMAKE_SOURCE_DIR}/include)

# Link libraries
target_link_libraries(tests PRIVATE Catch2::Catch2 Threads::Threads)

# Add test
add_test(NAME DroneDQN_Tests COMMAND tests)