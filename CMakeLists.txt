cmake_minimum_required(VERSION 3.10)
project(cross_isa_gemm)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "-O3")

include_directories(include)

add_executable(gemm_bench
    src/main.cpp
    src/gemm_naive.cpp
    src/gemm_blocked.cpp
    src/timer.cpp
)
