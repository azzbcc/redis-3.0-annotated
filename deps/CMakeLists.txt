cmake_minimum_required(VERSION 2.6)
if (POLICY CMP0048)
    cmake_policy(SET CMP0048 NEW)
endif(POLICY CMP0048)

find_package(PkgConfig REQUIRED)

#### 编译 hiredis 依赖 ####
pkg_check_modules(HR hiredis)
if (NOT HR_FOUND)
    set(hiredis_srcs
        hiredis/async.c
        hiredis/hiredis.c
        hiredis/net.c
    )
    add_library(hiredis ${hiredis_srcs})
    set(HR_LIBRARIES hiredis PARENT_SCOPE)
    set(HR_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/hiredis PARENT_SCOPE)
endif()
##########################

#### 编译 linenoise 依赖 ####
set(linenoise_srcs
    linenoise/linenoise.c
)
add_library(linenoise ${linenoise_srcs})
set(LN_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/linenoise PARENT_SCOPE)
set(LN_LIBRARIES linenoise PARENT_SCOPE)
##########################

#### 编译 lua 依赖 ####
pkg_check_modules(LUA luajit)
set(lua_extra_srcs
    lua/src/lua_cmsgpack.c
    lua/src/lua_cjson.c
    lua/src/lua_struct.c
    lua/src/strbuf.c
)
if (LUA_FOUND)
    add_library(lua-extra ${lua_extra_srcs})

    set(LUA_LIBRARIES "${LUA_LIBRARIES};lua-extra" PARENT_SCOPE)
else()
    set(lua_srcs
        ${lua_extra_srcs}
        lua/src/lapi.c
        lua/src/lauxlib.c
        lua/src/lbaselib.c
        lua/src/lcode.c
        lua/src/ldblib.c
        lua/src/ldebug.c
        lua/src/ldo.c
        lua/src/ldump.c
        lua/src/lfunc.c
        lua/src/lgc.c
        lua/src/llex.c
        lua/src/lmathlib.c
        lua/src/lmem.c
        lua/src/lobject.c
        lua/src/lopcodes.c
        lua/src/lparser.c
        lua/src/lstate.c
        lua/src/lstring.c
        lua/src/lstrlib.c
        lua/src/ltable.c
        lua/src/ltablib.c
        lua/src/ltm.c
        lua/src/lua.c
        lua/src/lundump.c
        lua/src/lvm.c
        lua/src/lzio.c
    )
    add_library(lua ${lua_srcs})

    set(LUA_LIBRARIES lua PARENT_SCOPE)
    set(LUA_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/lua/src PARENT_SCOPE)
endif()
##########################