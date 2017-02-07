find_package (GMock)
include_directories (${GMOCK_INCLUDE_DIRS})

###
###  General setup
###

include_directories (${CMAKE_SOURCE_DIR})
#include_directories (${CMAKE_CURRENT_BINARY_DIR})

set (CMAKE_C_FLAGS   "${CMAKE_C_FLAGS}   -g ${CC_WARNING_ARGS}")
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g ${CC_WARNING_ARGS} -std=c++11")

add_test(NAME formatcode 
         COMMAND "${CMAKE_SOURCE_DIR}/tools/format-test.sh" "${CMAKE_SOURCE_DIR}" "${CMAKE_BINARY_DIR}/tools/formatcode")

###
###  phone-test
###

set (TEST_NAME phone-test)
add_executable (${TEST_NAME} ${TEST_NAME}.cc)
add_test (${TEST_NAME} ${TEST_NAME})
add_dependencies (${TEST_NAME} ${SERVICE_LIB})
target_link_libraries (${TEST_NAME}
  ${SERVICE_LIB}
  ${SERVICE_DEPS_LIBRARIES}

  ${GMOCK_LIBRARIES}
)
