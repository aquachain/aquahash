cmake_minimum_required(VERSION 3.8)
project(AQUAHASH C)

set(USE_AVX2 ON)
set(USE_NATIVE OFF)
set(SRC
  src/argon2.c src/core.c src/blake2/blake2b.c src/thread.c src/encoding.c)

if(${USE_AVX2}==ON)
  set(SRC ${SRC} src/opt.c)
else()
  set(SRC ${SRC} src/ref.c)
endif()

add_library(aquahash
  ${SRC})
target_include_directories(aquahash
  PUBLIC
  include/aquahash)

if(${USE_NATIVE}==ON)
    target_compile_options(aquahash
      PUBLIC
      -march=native)
endif()
