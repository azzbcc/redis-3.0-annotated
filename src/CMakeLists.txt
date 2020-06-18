cmake_minimum_required(VERSION 2.6)
if (POLICY CMP0048)
    cmake_policy(SET CMP0048 NEW)
endif(POLICY CMP0048)

include(CMakeLists.release.txt)

include_directories(
    ${HR_INCLUDE_DIRS}
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