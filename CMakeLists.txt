project(game.libretro.beetle-pce-fast)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(Kodi REQUIRED)
find_package(libretro-beetle-pce-fast REQUIRED)

set(DEPLIBS beetle-pce-fast)
set(BEETLE_PCE_FAST_CUSTOM_BINARY ${BEETLE_PCE_FAST_LIB}
                                  game.libretro.beetle-pce-fast${CMAKE_SHARED_LIBRARY_SUFFIX} beetle-pce-fast)

build_addon(game.libretro.beetle-pce-fast BEETLE_PCE_FAST DEPLIBS)

