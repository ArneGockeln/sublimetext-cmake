# set additional cxx flags
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
# set local include directory
#include_directories(/usr/local/include)

# add source files for your binary
add_executable(${PROJECT_NAME} main.cpp)

# copy binary to parent directory build/
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:${PROJECT_NAME}> ../)