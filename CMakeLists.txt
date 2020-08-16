PROJECT(sqlite3)
cmake_minimum_required(VERSION 3.5)

add_library(sqlite3 STATIC sqlite3.c sqlite3.h sqlite3ext.h)
target_compile_definitions(sqlite3 PUBLIC SQLITE_ENABLE_RTREE)
target_compile_definitions(sqlite3 PUBLIC SQLITE_ENABLE_JSON1)

find_package(Threads REQUIRED)

add_executable(sqlite sqlite3.c shell.c sqlite3.h sqlite3ext.h)
set_target_properties(sqlite PROPERTIES OUTPUT_NAME sqlite3)
target_link_libraries(sqlite Threads::Threads ${CMAKE_DL_LIBS})

install(FILES sqlite3.h sqlite3ext.h DESTINATION include)
install(TARGETS sqlite3 LIBRARY DESTINATION lib ARCHIVE DESTINATION lib)
install(TARGETS sqlite RUNTIME DESTINATION bin)
