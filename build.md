# 搭建 mud 游戏服务器

## FLuffos 下载和编译

Fluffos 是 LPMUD 游戏驱动，目前有2017和2019二个主要版本，2017版可以直接驱动现有的MUD游戏，但2019版只支持utf-8的mudlib,本教程使用的是v2019版驱动，使用 `cmake` 编译。

### 编译环境配置

请直接复制以下命令并运行。
```
sudo apt update
sudo apt install libjemalloc-dev bison zlib1g-dev libssl-dev libmysqlclient-dev libpcre3-dev libevent-dev libicu-dev gcc g++ autoconf automake cmake -y
```

> <checker type="output-contains" command="cmake" hint="请安装 cmake">
>    <keyword regex="cmake --help" />
> </checker>

### 下载 FLuffos 源码

[fluffos](https://github.com/fluffos/fluffos) 下载。

#### 下载
```
git clone https://github.com/fluffos/fluffos.git
```

> <checker type="output-contains" command="ls -la ~" hint="请下载fluffos">
>    <keyword regex="fluffos" />
> </checker>

### 编译 Fluffos 驱动
```
cd ~/fluffos && mkdir build && cd build && cmake .. && make install && cd bin
```
安装完成会在 `~/fluffos/build/bin` 目录中生成驱动文件 `driver`。
> <checker type="output-contains" command="ls ~/fluffos/build/bin" hint="编译 driver">
>    <keyword regex="driver" />
> </checker>

## MUD 游戏服务启动

### MUD 源码下载

MUD 游戏驱动需要配合 MUDLIB 运行，这里使用开源的炎黄 MUD，可直接建站。

#### 下载

使用 `git` clone 游戏服务端源码
```
cd ~ && git clone https://github.com/oiuv/mud.git
```

> <checker type="output-contains" command="ls ~" hint="请下载mud源码">
>    <keyword regex="mud" />
> </checker>

### 移动驱动到游戏源码目录
```
cd ~/mud && cp ~/fluffos/build/bin/driver .
```

> <checker type="output-contains" command="ls ~/mud" hint="请移动驱动到游戏目录">
>    <keyword regex="driver" />
> </checker>

### MUD 服务器启动
```
./driver config.ini
```

至此服务器启动，可以在客户端连接：
```
telnet ${runtime.vars.cvmIpAddress} 3160
```

或者使用其它mud游戏客户端登录游戏。

请注意：使用 `mudren` 为ID注册登录游戏为管理员，可以在游戏中使用 `shutdown` 指令关闭服务器。

> <checker type="output-contains" command="ls ~/mud-master/log" hint="请启动服务器">
>    <keyword regex="debug.log" />
> </checker>
