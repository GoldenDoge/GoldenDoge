# GoldenDoge
## About

Welcome to the repository of GoldenDoge. 🐶 ... such a currency
if you don't want to compile it you can download compiled binaries [here](https://github.com/GoldenDoge/GoldenDoge/releases)

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
    $GoldenDoge/boost> ./b2 link=static -j 2 --build-dir=build64 --stagedir=stage
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
Create build directory inside `GoldenDoge`, go there and run CMake and Make:
```
$GoldenDoge> cd GoldenDoge
$GoldenDoge/GoldenDoge> mkdir build
$GoldenDoge/GoldenDoge> cd build
$GoldenDoge/GoldenDoge/build> cmake ..
$GoldenDoge/GoldenDoge/build> time make -j2 (2 is an example, it is the number of CPU threads)
```
     
Check built binaries by running them from `../bin` folder
```
$GoldenDoge/GoldenDoge/build> ../bin/./GoldenDoged -v
```

### Building with specific options

Download amalgamated [SQLite 3](https://www.sqlite.org/download.html) and unpack it into `GoldenDoge/sqlite` folder (source files are referenced via relative paths, so you do not need to separately build it).

Below are the commands which remove OpenSSL support and switch from LMDB to SQLite by providing options to CMake:

```
$GoldenDoge/GoldenDoge> mkdir build
$GoldenDoge/GoldenDoge cd build
$GoldenDoge/GoldenDoge/build> cmake -DUSE_SSL=0 -DUSE_SQLITE=1 ..
$GoldenDoge/GoldenDoge/build> time make -j2 (2 is an example, it is the number of CPU threads)
```

## Building on Windows

You need Microsoft Visual Studio Community 2017. [Download](https://www.visualstudio.com/vs/) and install it selecting `C++`, `git`, `cmake integration` packages.
Run `Visual Studio x64 command prompt` from start menu.

Create directory `GoldenDoge` somewhere:
```
$C:\> mkdir GoldenDoge
$C:\> cd GoldenDoge
```

Get [Boost](https://boost.org) and unpack it into a folder inside `GoldenDoge` and rename it from `boost_1_66_0` or similar to just `boost`.

Build boost.
```
$> cd boost
$C:\GoldenDoge\boost> bootstrap.bat
$C:\GoldenDoge\boost> b2.exe address-model=64 link=static -j 2 --build-dir=build64 --stagedir=stage
$C:\GoldenDoge\boost> b2.exe address-model=32 link=static -j 2 --build-dir=build32 --stagedir=stage32
cd ..
```

* Clone GoldenDoge source code from github in that folder:
```
$C:\GoldenDoge> git clone https://github.com/GoldenDoge/GoldenDoge
```

Download [SQLite 3](https://www.sqlite.org/download.html) source code and unpack it into `GoldenDoge/sqlite` folder (source files are referenced via relative paths, so you do not need to separately build it).

* Create build directory inside `GoldenDoge`, go there and run CMake and make it:
```
$C:\GoldenDoge> cd GoldenDoge
$C:\GoldenDoge\GoldenDoge> copy ..\sqlite\shell.c src\shell.c /y
$C:\GoldenDoge\GoldenDoge> copy ..\sqlite\sqlite3.c src\sqlite3.c /y
$C:\GoldenDoge\GoldenDoge> copy ..\sqlite\sqlite3.h src\sqlite3.h /y
$C:\GoldenDoge\GoldenDoge> copy ..\sqlite\sqlite3ext.h src\sqlite3ext.h /y
$C:\GoldenDoge\GoldenDoge> mkdir build
$C:\GoldenDoge\GoldenDoge> cd build
$C:\GoldenDoge\GoldenDoge\build> cmake -DUSE_SSL=0 -DUSE_SQLITE=1 ..
```

Now you can open GoldenDoge.sln in build folder in VisualStudio 2017 and build it

