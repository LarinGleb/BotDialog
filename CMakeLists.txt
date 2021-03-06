cmake_minimum_required(VERSION 2.8.4)
project(DialogBot)


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall")
set(Boost_USE_MULTITHREADED ON)


find_package(Threads REQUIRED)
find_package(OpenSSL REQUIRED)
find_package(Boost COMPONENTS system REQUIRED)
find_package(CURL)


include_directories(/usr/local/include ${OPENSSL_INCLUDE_DIR} ${Boost_INCLUDE_DIR})

add_executable(Dialog Bot.cpp)

add_subdirectory(Connector)
message("Included connector")

add_subdirectory(BotTools)
message("Included bot tools")

add_subdirectory(ReviewBot)
message("Included Review Bot")

target_link_libraries(Dialog DataBaseLib)
target_link_libraries(Dialog Tools)
target_link_libraries(Dialog ReviewBot)

target_link_libraries(Dialog /usr/local/lib/libTgBot.a ${CMAKE_THREAD_LIBS_INIT} ${OPENSSL_LIBRARIES} ${Boost_LIBRARIES} ${CURL_LIBRARIES})


add_dependencies(Dialog DataBaseLib)
add_dependencies(Dialog Tools) 
add_dependencies(Dialog ReviewBot)