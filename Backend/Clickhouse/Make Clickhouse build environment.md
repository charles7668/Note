# Make Clickhouse build environment

this note using Ubuntu22.04 os

## Index

- [Make Clickhouse build environment](#make-clickhouse-build-environment)
  - [Index](#index)
  - [install build-essential](#install-build-essential)
  - [install clang](#install-clang)
  - [install lld](#install-lld)
  - [install pthread](#install-pthread)
    - [Reference](#reference)
  - [install nasm](#install-nasm)
  - [install yasm](#install-yasm)
  - [disable cache](#disable-cache)

## install build-essential

- `sudo apt update && sudo apt install build-essential`

## install clang

- download install script by `wget https://apt.llvm.org/llvm.sh`
- add executable permission `chmod u+x llvm.sh`
- install using `sudo ./llvm.sh 17`
- verify install `clang-17 --version`
- add `-DCMAKE_C_COMPILER=clang-17` and `-DCMAKE_CXX_COMPILER=clang-17` in cmake build option

## install lld

- `sudo apt update && sudo apt install lld`

## install pthread

- `sudo apt update && sudo apt-get install libpthread-stubs0-dev`
- set following setting in CMakelist.txt or using `-D` in command line

  ```bash
  -DCMAKE_THREAD_LIBS_INIT="-lpthread"
  -DCMAKE_HAVE_THREADS_LIBRARY=1
  -DCMAKE_USE_WIN32_THREADS_INIT=0
  -DCMAKE_USE_PTHREADS_INIT=1
  -DTHREADS_PREFER_PTHREAD_FLAG=ON
  ```

### Reference

- [Could NOT find Threads (missing: Threads_FOUND) · Issue #2 · alicevision/geogram](https://github.com/alicevision/geogram/issues/2)

## install nasm

- `sudo apt update && sudo apt install nasm`

## install yasm

- `sudo apt update && sudo apt install yasm`

## disable cache

- `-DCOMPILER_CACHE=disabled`
