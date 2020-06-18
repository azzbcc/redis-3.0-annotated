cmake_minimum_required(VERSION 2.6)
if (POLICY CMP0048)
    cmake_policy(SET CMP0048 NEW)
endif(POLICY CMP0048)

include(CMakeLists.release.txt)

include_directories(
    ${HR_INCLUDE_DIRS}
    ${LN_INCLUDE_DIRS}
    ${LUA_INCLUDE_DIRS}
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

set(redis_server_srcs
    adlist.c
    ae.c
    anet.c
    aof.c
    bio.c
    bitops.c
    blocked.c
    cluster.c
    config.c
    crc16.c
    crc64.c
    db.c
    debug.c
    dict.c
    endianconv.c
    hyperloglog.c
    intset.c
    lzf_c.c
    lzf_d.c
    memtest.c
    multi.c
    networking.c
    notify.c
    object.c
    pqsort.c
    pubsub.c
    rand.c
    rdb.c
    redis.c
    release.c
    replication.c
    rio.c
    scripting.c
    sds.c
    sentinel.c
    setproctitle.c
    sha1.c
    slowlog.c
    sort.c
    syncio.c
    t_hash.c
    t_list.c
    t_set.c
    t_string.c
    t_zset.c
    util.c
    ziplist.c
    zipmap.c
    zmalloc.c
)
set(redis_server_deps
    pthread
    m
    ${HR_LIBRARIES}
    ${LUA_LIBRARIES}
)
message(STATUS "redis_server_deps: ${redis_server_deps}")

add_executable(redis-server ${redis_server_srcs})
target_link_libraries(redis-server ${redis_server_deps})