cmake_minimum_required(VERSION 2.6)
if (POLICY CMP0048)
    cmake_policy(SET CMP0048 NEW)
endif(POLICY CMP0048)

project(redis_3_0_annotated C)

add_subdirectory(deps)
add_subdirectory(src)