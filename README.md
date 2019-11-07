# GoldenDoge
## About

Welcome to the repository of GoldenDoge. 🐶 ... such a currency

## Contents
* Building on Linux 64-bit
* Building on Windows

## Building on Linux 64-bit

Command here are adapted for ubuntu linux ,you might write different commands on other distributions!!!

Create directory `GoldenDoge` and go there:
```
$> mkdir GoldenDoge
$> cd GoldenDoge
```

To go futher you have to have a number of packages and utilities. You need at least gcc 5.4.
* `build-essential` package:
    ```
    $GoldenDoge> sudo apt-get install build-essential
    ```
* `git` package:
    ```
    $GoldenDoge> sudo apt-get install git
    ```    
* CMake (3.5 or newer):
    ```
    $GoldenDoge> sudo apt-get install cmake
    $GoldenDoge> cmake --version
    ```
    If version is too old, follow instructions on [the official site](https://cmake.org/download/).
* Boost (1.62 or newer):
    You need boost in `GoldenDoge` folder. We do not configure to use boost installed by `apt-get`, because it is sometimes updated without your control by installing some unrelated packages. Also some users reported crashes after `find_package` finds headers from one version of boost and libraries from different version, or if installed boost uses dynamic linking.
    ```
    $GoldenDoge> wget -c 'http://sourceforge.net/projects/boost/files/boost/1.67.0/boost_1_67_0.tar.bz2/download'
    $GoldenDoge> tar xf download
    $GoldenDoge> rm download
    $GoldenDoge> mv boost_1_67_0 boost
    $GoldenDoge> cd boost
    $GoldenDoge/boost> ./bootstrap.sh
    $GoldenDoge/boost> ./b2 link=static -j 8 --build-dir=build64 --stagedir=stage
    cd ..
    ```
* OpenSSL (1.1.1 or newer):
    Install OpenSSL to `GoldenDoge/openssl` folder. (In below commands use switch `linux-x86_64-clang` instead of `linux-x86_64` if using clang.)
    ```
    $GoldenDoge> git clone https://github.com/openssl/openssl.git
    $GoldenDoge> cd openssl
    $GoldenDoge/openssl> ./Configure linux-x86_64 no-shared
    $GoldenDoge/openssl> time make -j2
    $GoldenDoge/openssl> cd ..
    ```
    
* Clone GoldenDoge source code from github in that folder:
     ```
     $GoldenDoge> git clone https://github.com/GoldenDoge/GoldenDoge
     ```
