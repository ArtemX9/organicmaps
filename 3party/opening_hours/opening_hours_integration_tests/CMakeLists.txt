project(opening_hours_integration_tests)

set(SRC opening_hours_integration_tests.cpp)

omim_add_executable(${PROJECT_NAME} ${SRC})

target_link_libraries(${PROJECT_NAME} opening_hours)

if(${CMAKE_SYSTEM_NAME} MATCHES "Linux") 
  set(COPY_CMD cp -u)
else()
  set(COPY_CMD rsync -a)
endif()

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
  COMMAND ${COPY_CMD} "${CMAKE_CURRENT_SOURCE_DIR}/opening-count.lst" "${CMAKE_BINARY_DIR}/"
  COMMENT "Copying opening-count.lst file for testing"
)
