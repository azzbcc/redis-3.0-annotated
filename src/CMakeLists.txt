cmake_minimum_required(VERSION 2.6)
if (POLICY CMP0048)
    cmake_policy(SET CMP0048 NEW)
endif(POLICY CMP0048)

include(CMakeLists.release.txt)

include_directories(
    ${HR_INCLUDE_DIRS}
    ${LN_INCLUDE_DIRS}
    ${CMAKE_CURRENT_BINARY_DIR}
)

set(redis_benchmark_srcs
    ae.c
    adlist.c
    redis-benchmark.c
    sds.c
    zmalloc.c
)
set(redis_benchmark_deps
    ${HR_LIBRARIES}
)

add_executable(redis-benchmark ${redis_benchmark_srcs})
target_link_libraries(redis-benchmark ${redis_benchmark_deps})

set(redis_cli_srcs
    ae.c
    anet.c
    crc64.c
    redis-cli.c
    release.c
    sds.c
    zmalloc.c
)
set(redis_cli_deps
    ${HR_LIBRARIES}
    ${LN_LIBRARIES}
)

add_executable(redis-cli ${redis_cli_srcs})
target_link_libraries(redis-cli ${redis_cli_deps})