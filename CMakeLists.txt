cmake_minimum_required(VERSION 3.14) # Ensure you have a minimum version that supports FetchContent

project(your_project_name) # Replace your_project_name with your actual project name

# Include FetchContent module to download Google Test
include(FetchContent)

# Declare GoogleTest as a fetch content
FetchContent_Declare(
  googletest
  # Specify the commit you want to fetch from the GoogleTest repository
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG release-1.11.0 # You can adjust this to the specific version you want
)

# Make GoogleTest available for use
FetchContent_MakeAvailable(googletest)

enable_testing()

# Define your test executable
add_executable(
  token_tests
  token_tests.cc
  token.c
  int_stack.c
)

# Link the Google Test main entry point
target_link_libraries(
  token_tests
  gtest_main
  pthread # Changed from -lpthread for clarity and consistency
)

# Define your other executables as before
add_executable(
  tokenInput
  main.c
  token.c
)
target_link_libraries(
  tokenInput
  m # Changed from -lm for clarity and consistency
)

add_executable(
  stackDemo
  int_stack_demo.c
  int_stack.c
)
target_link_libraries(
  stackDemo
  m # Changed from -lm for clarity and consistency
)

# Include GoogleTest's utilities for easier test discovery and execution
include(GoogleTest)
gtest_discover_tests(token_tests)
