project(game.libretro.beetle-pce-fast)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)

include(ExternalProject)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(LIBRETRO_DEBUG DEBUG=1)
endif()

if("${CORE_SYSTEM_NAME}" STREQUAL "windows")
  set(BUILD_COMMAND mingw32-make platform=win ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "linux")
  set(BUILD_COMMAND make ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "darwin")
  set(BUILD_COMMAND make platform=osx ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "ios")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "android")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "rbpi")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "freebsd")
# TODO
endif()

externalproject_add(beetle-pce-fast
                    GIT_REPOSITORY https://github.com/libretro/beetle-pce-fast-libretro
                    GIT_TAG 3567dee
                    PREFIX beetle-pce-fast
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND ${BUILD_COMMAND}
                    BUILD_IN_SOURCE 1)

set(BEETLEPCE_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/beetle-pce-fast/src/beetle-pce-fast/mednafen_pce_fast_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                            game.libretro.beetle-pce-fast${CMAKE_SHARED_LIBRARY_SUFFIX} beetle-pce-fast)

build_addon(game.libretro.beetle-pce-fast BEETLEPCE DEPLIBS)
add_dependencies(game.libretro.beetle-pce-fast beetle-pce-fast)

include(CPack)
