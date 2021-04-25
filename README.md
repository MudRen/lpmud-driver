## lpmud-driver - [fluffos](https://github.com/fluffos/fluffos)

### 文件说明

 - [v2019.cfg](v2019.cfg) - 运行时配置文件 utf-8 版，fluffos v2019 专用
 - [v2017.cfg](v2017.cfg) - 运行时配置文件 GBK 版，旧版驱动和 fluffos v2017 使用
 - [local_options](local_options) - fluffos v2019 配置文件
 - [local_options.h](local_options.h) - fluffos v2017 配置文件
 - [local_options.README](local_options.README) - fluffos v2017 配置文件注释版

### 编译说明

最新版编译指南请点这里：[FluffOS在windows和ubuntu/centos/mac系统下的编译](https://bbs.mud.ren/threads/2)

不管是 v2017 还是 v2019，编译配置文件都为 `src` 下面的 `local_options` 文件，请根据需要修改（非特别需求，推荐使用默认配置）。

```
$ git clone https://github.com/fluffos/fluffos.git
$ cd fluffos
$ git checkout v2019 (or v2017)
```

### UBUNTU 编译

#### 系统环境配置

编译前请执行以下指令安装必要的包。

```
$ sudo apt install libjemalloc-dev bison zlib1g-dev libssl-dev libmysqlclient-dev libpcre3-dev libevent-dev libicu-dev gcc g++ autoconf automake cmake -y
```

#### v2017编译指令

```
$ cd src
$ ./build.FluffOS
$ make install
```
编译好的驱动程序 `driver` 在 `bin` 目录中。

#### v2019编译指令

```
$ mkdir build && cd build
$ cmake ..
$ make install
```
编译好的驱动程序 `driver` 在 `build/bin` 目录中。

注意，如果不需要某个包，请使用类似以下指令编译：

> cmake -DPACKAGE_DB=OFF ..

默认编译为动态编译，仅针对当前CPU优化，如果需要静态编译，请使用以下指令编译：

> cmake -DMARCH_NATIVE=OFF -DSTATIC=ON ..

### MACOS 编译

仅支持 v2019 最新版，需要执行以下指令安装必要的包。

```
brew install cmake pkg-config mysql pcre libgcrypt libevent openssl jemalloc icu4c
```

build same as under linux, you will need to pass two environment variables

```
$ make build && cd build
$ OPENSSL_ROOT_DIR="/usr/local/opt/openssl" ICU_ROOT="/usr/local/opt/icu4c" cmake ..
$ make install
```

### MSYS2 编译说明

v2019版支持 MSYS2 下编译，官方网站：https://www.msys2.org/ 下载安装后需运行 Mingw-w64 64 bit，更新系统并安装必须的包，国外镜像速度慢，可以先根据以下配置修改为国内镜像：

#### pacman 的配置

编辑 /etc/pacman.d/mirrorlist.mingw32 ，在文件开头添加：

    Server = http://mirrors.ustc.edu.cn/msys2/mingw/i686

编辑 /etc/pacman.d/mirrorlist.mingw64 ，在文件开头添加：

    Server = http://mirrors.ustc.edu.cn/msys2/mingw/x86_64

编辑 /etc/pacman.d/mirrorlist.msys ，在文件开头添加：

    Server = http://mirrors.ustc.edu.cn/msys2/msys/$arch

然后执行 `pacman -Syu` 刷新软件包数据即可。

#### 系统配置

```
$ pacman -Syu
$ pacman -S git make mingw-w64-x86_64-toolchain mingw-w64-x86_64-cmake
$ pacman -S mingw-w64-x86_64-zlib mingw-w64-x86_64-libevent mingw-w64-x86_64-pcre mingw-w64-x86_64-icu
$ pacman -S bison
```

#### 编译指令

```
$ mkdir build
$ cd build
$ cmake -G "MSYS Makefiles" -DPACKAGE_CRYPTO=OFF -DPACKAGE_DB=OFF ..
$ make install
```

### CYGWIN 编译说明

v2017版支持 CYGWIN 下编译，官方网站：http://cygwin.org/ 下载后需要安装以下包，编译方式和其它系统一样。

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
- libmysqlclient-devel
- libpcre-devel
- make
- python3
- zlib-devel
