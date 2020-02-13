cmake_minimum_required(VERSION 3.1)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/third_party/gate/cmake)

set(
        CMAKE_TOOLCHAIN_FILE
        "${CMAKE_SOURCE_DIR}/third_party/polly/gcc-7-cxx14-pic.cmake"
)

set(
        CMAKE_TOOLCHAIN_FILE
        "${CMAKE_SOURCE_DIR}/third_party/polly/gcc-7-cxx14-pic.cmake"
)

set(HUNTER_USE_CACHE_SERVERS YES)
set(HUNTER_RUN_UPLOAD ON)
set(HUNTER_JOBS_NUMBER 6 CACHE STRING "Hunter jobs number")


include(HunterGate)
HunterGate(
        URL "https://github.com/ruslo/hunter/archive/v0.23.214.tar.gz"
        SHA1 "e14bc153a7f16d6a5eeec845fb0283c8fad8c358"
        FILEPATH ${CMAKE_SOURCE_DIR}/cmake/Hunter/config.cmake
)
include(hunter_add_package)
include(hunter_add_version)
include(hunter_cacheable)
include(hunter_cmake_args)
include(hunter_download)
include(hunter_pick_scheme)

project(rocksplicator)

hunter_add_package(folly)
find_package(folly CONFIG REQUIRED)

#set(CMAKE_CXX_FLAGS "-std=c++17 -gdwarf-2 -O3 -Wall -fPIC -fno-omit-frame-pointer")

include_directories(/usr/local/include)
include_directories(/usr/lib/jvm/java-8-openjdk-amd64/include)
include_directories(/usr/lib/jvm/java-8-openjdk-amd64/include/linux/)
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories("${CMAKE_CURRENT_SOURCE_DIR}/build")

link_directories("/usr/local/lib/linux/intel64/Release/")
link_directories("/usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/server/")

enable_testing()

# submodules
add_subdirectory(googletest)

# Sub-projects
add_subdirectory(common)
add_subdirectory(examples)
add_subdirectory(rocksdb_admin)
add_subdirectory(rocksdb_replicator)
add_subdirectory(tgrep)
