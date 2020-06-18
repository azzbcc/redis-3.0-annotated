cmake_minimum_required(VERSION 2.6)
if (POLICY CMP0048)
    cmake_policy(SET CMP0048 NEW)
endif(POLICY CMP0048)

find_package(PkgConfig REQUIRED)

#### 编译 hiredis 依赖 ####
pkg_check_modules(HR hiredis)
if (NOT HR_FOUND)
    set(hiredis_srcs
        hiredis/hiredis.c
        hiredis/net.c
    )
    add_library(hiredis ${hiredis_srcs})
    set(HR_LIBRARIES hiredis PARENT_SCOPE)
    set(HR_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/hiredis PARENT_SCOPE)
endif()
##########################