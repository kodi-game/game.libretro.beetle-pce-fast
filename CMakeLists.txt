cmake_minimum_required(VERSION 3.1)
project(game.libretro.beetle-pce-fast)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

find_package(Kodi REQUIRED)
find_package(libretro-beetle-pce-fast REQUIRED)

set(BEETLE-PCE-FAST_CUSTOM_BINARY ${BEETLE-PCE-FAST_LIB}
    ${PROJECT_NAME}${CMAKE_SHARED_LIBRARY_SUFFIX})

build_addon(${PROJECT_NAME} BEETLE-PCE-FAST "")
