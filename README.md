# Docker Images for C++ CI Workflows

This repository provides two Docker images optimized for use in GitHub Actions 
CI workflows targeting C++ projects.

## Available Images

### 1. [`ghcr.io/mattkretz/cplusplus-ci/base`](https://github.com/users/mattkretz/packages/container/package/cplusplus-ci%2Fbase)

A base image built on **Ubuntu 24.04**, with several useful packages installed 
via APT:

- `make` and `ninja`
- `cmake`
- GCC 13 and 14 with `-m32` and `-mx32` support
- Default `gcc`/`g++` → **GCC 14**
- Clang 20 and 21 (trunk)

You can set the `CXX` environment variable to:

- `g++-13`
- `g++-14`
- `clang++-20`
- `clang++-21`

---

### 2. [`ghcr.io/mattkretz/cplusplus-ci/latest`](https://github.com/users/mattkretz/packages/container/package/cplusplus-ci%2Flatest)

This image builds on the `base` image and adds:

- **GCC 15** and **GCC master**, compiled from the upstream `releases/gcc-15` 
  and `master` branches
- Installed in:
  - `/opt/gcc-15`
  - `/opt/gcc-master`
- Supports `-m32` and `-mx32` builds
- Default `gcc`/`g++` → **GCC 15**

You can additionally set the `CXX` environment variable to:

- `g++-15`
- `g++-master` *(alias: `g++-trunk`)*

---

## Example GitHub CI Workflow

```yaml
name: Clang

on:
  push:
    branches: [ main ]
  pull_request:

jobs:
  clang:
    strategy:
      fail-fast: false
      matrix:
        version: [20, 21]

    runs-on: ubuntu-latest

    container:
      image: ghcr.io/mattkretz/cplusplus-ci/base

    steps:
      - uses: actions/checkout@v4

      - name: Run test suite
        env:
          CXX: clang++-${{ matrix.version }}
        run: make check
```
