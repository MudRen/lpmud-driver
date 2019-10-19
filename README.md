## lpmud-driver - [fluffos](https://github.com/fluffos/fluffos)

### 文件说明

 - [config.ini](config.ini) - 运行时配置文件 utf-8 版
 - [local_options](local_options) - fluffos v2019 配置文件
 - [local_options.h](local_options.h) - fluffos v2017 配置文件
 - [local_options.README](local_options.README) - fluffos v2017 配置文件注释版

### 系统环境配置

编译前请执行以下指令安装必要的包。

```
$ sudo apt install libjemalloc-dev bison zlib1g-dev libssl-dev libmysqlclient-dev libpcre3-dev libevent-dev cmake cargo autoconf automake -y
```

### 编译说明

不管是 v2017 还是 v2019，编译配置文件都为 `src` 下面的 `local_options` 文件，请根据需要修改（非特别需求，推荐使用默认配置）。

```
$ git clone https://github.com/fluffos/fluffos.git
$ cd fluffos
$ git checkout v2019 (or v2017)
```

#### v2017编译指令

```
$ cd src
$ ./build.FluffOS
$ make
$ make install
```
编译好的驱动程序 `driver` 在 `bin` 目录中。

#### v2019编译指令

**2019 年 10 月以前的版本，请用 `cmake` 编译**：

```
$ git reset --hard c8f24e89b3f4d6df77d9bf0bab4aa6c66ce041c2
$ mkdir build && cd build
$ cmake ..
$ make
```
编译好的驱动程序 `driver` 在 `build/src` 目录中。

注意，如果不需要某个包，请使用类似以下指令编译：

> cmake -DPACKAGE_DB=OFF ..

默认编译为动态编译，仅针对当前CPU优化，如果需要静态编译，请使用以下指令编译：

> cmake -DMARCH_NATIVE=OFF -DSTATIC=ON ..

**最新版本请用 `cargo` 编译**：

```
$ cargo build -vvv
```
编译好的驱动程序在 `target/debug` 目录中，包括 `fluffos` 和 `libdriver.so` 二个文件。

注意，如果不需要某个包，请修改对应包的 `src/packages/XXX/CMakeLists.txt` 文件中的 `ON` 为 `OFF` 。


#### CYGWIN 编译说明

CYGWIN 下编译需要安装以下包，编译方式和其它系统一样。目前CYGWIN下编译2019版本仅支持 cmake 编译方式，不支持最新版。

- autoconf
- automake
- binutils
- bison
- cmake
- gcc-core
- gcc-g++
- git
- libcrypt-devel
- libevent-devel
- libiconv-devel
- libicu-devel
- libmariadb-devel
- libmysqlclient-devel
- libpcre-devel
- make
- python3
- zlib-devel
