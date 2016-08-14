cmake_minimum_required(VERSION 2.8)
project (LexYacc)

find_package(BISON)
find_package(FLEX)

BISON_TARGET(MyParser src/mcc2.y ${CMAKE_CURRENT_BINARY_DIR}/y.tab.c) 
FLEX_TARGET(MyScanner src/mcc2.l  ${CMAKE_CURRENT_BINARY_DIR}/lex.yy.c)
ADD_FLEX_BISON_DEPENDENCY(MyScanner MyParser)

include_directories(${CMAKE_CURRENT_BINARY_DIR})
add_executable(LexYacc
  ${BISON_MyParser_OUTPUTS}
  ${FLEX_MyScanner_OUTPUTS})
target_link_libraries(LexYacc ${FLEX_LIBRARIES} ${BISON_LIBRARIES})
