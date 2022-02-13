cmake_minimum_required(VERSION 3.10)

project(client VERSION 0.1)

aux_source_directory(${PROJECT_SOURCE_DIR}/rcssbase/gzip GZIP)
aux_source_directory(${PROJECT_SOURCE_DIR}/rcssbase/net NET)

add_definitions(-DHAVE_CONFIG_H)

# SET(CMAKE_CXX_FLAGS -lrcsc -lrcsc -L${PROJECT_SOURCE_DIR}/rcssbase/net -L${PROJECT_SOURCE_DIR}/rcssbase/gzip -lboost)

add_executable(client
    ${GZIP}
    ${NET}
    client.cpp
    )

target_include_directories(client
    PUBLIC
    ${PROJECT_SOURCE_DIR}
    ${PROJECT_SOURCE_DIR}/rcssbase/gzip
    ${PROJECT_SOURCE_DIR}/rcssbase/net
    )


# boost
find_package(Boost 1.36.0 COMPONENTS system REQUIRED)
if(NOT Boost_FOUND)
  message(FATAL_ERROR "Boost not found!")
endif()

# zlib
find_package(ZLIB)
if(ZLIB_FOUND)
  #add_definitions(-DHAVE_LIBZ)
  set(HAVE_LIBZ TRUE)
endif()


target_link_libraries(client
    PUBLIC
    Boost::system
    ZLIB::ZLIB
  )

