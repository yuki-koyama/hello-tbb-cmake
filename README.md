# Hello TBB CMake

A hello-world project for testing `parallel_for` in Intel(R) Threading Building Blocks (TBB). The whole project, including TBB, is built using CMake.

## How It Works

Wenzel Jakob (a great researcher) provides a repository containing TBB and CMake files for building TBB: <https://github.com/wjakob/tbb>. 

This hello-world repository includes Wenzel's TBB as a gitsubmodule, which is built using CMake's `ExternalProject_Add` command.

## Dependency

- <https://github.com/wjakob/tbb>

## Clone, Compile, and Run

### Clone

```
git clone https://github.com/yuki-koyama/hello-tbb-cmake.git --recursive
```

Do not forget to add the `--recursive` option.

### Compile

```
mkdir build
cd build
cmake ../hello-tbb-cmake
make
```

### Run

```
./hello-tbb-cmake
```

This program solves a numerical optimization problem 1,000,000 times with different initial solutions. First, it performs this task in parallel, and then it performs the same task in a single thread. Finally, it displays the elapsed times like:
```
parallel: 361 [ms]
serial:   1245 [ms]
```

## License

MIT License.

