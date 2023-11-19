# openGL setup

## 必备包

- cmake
- ninja
- gcc/g++

```sh
sudo pacman -S gcc
sudo pacman -S gcc-libs
sudo pacman -S gdb
```

- glfw3

```sh
sudo pacman -S glfw-x11
```

## glad 下载

[glad](https://glad.dav1d.de/)

## project 结构

```txt
.
├── CMakeLists.txt
├── glad.c
├── include
│   ├── glad
│   │   └── glad.h
│   └── KHR
│       └── khrplatform.h
└── main.cpp

4 directories, 5 files
```

## CMakeLists

```cmake
cmake_minimum_required(VERSION 3.17)

project(tri)

include_directories(include)
add_executable(${PROJECT_NAME} glad.c main.cpp)

target_link_libraries(${PROJECT_NAME} GL dl glfw)
```
