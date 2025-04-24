# Docker images for CI workflows in C++ projects

This repository provides two images for use in GitHub CI workflows in C++ 
projects.

1. [ghcr.io/mattkretz/cplusplus-ci/base](https://github.com/users/mattkretz/packages/container/package/cplusplus-ci%2Fbase)
    This container is based on Ubuntu 24.04 with several useful packages 
    installed via APT:

    - `make` and `ninja`
    - `cmake`
    - GCC 13 and 14 with `-m32` and `-mx32` support
    - `gcc`/`g++` defaults to GCC 14
    - Clang 20 and 21 (trunk)

    You can thus set your `CXX` environment variable to either one of:

    - `g++-13`
    - `g++-14`
    - `clang++-20`
    - `clang++-21`

2. [ghcr.io/mattkretz/cplusplus-ci/latest](https://github.com/users/mattkretz/packages/container/package/cplusplus-ci%2Flatest)
    This container builds upon the base image. In addition it has GCC 15 and 
    GCC trunk installed in `/opt/gcc-15` and `/opt/gcc-master`, respectively. 
    GCC is compiled from Git (`releases/gcc-15` and `master` branches).

    In this image `gcc`/`g++` defaults to GCC 15.

    In addition to the above, you can set your `CXX` environment variable to:

    - `g++-15`
    - `g++-master` (or `g++-trunk`)
