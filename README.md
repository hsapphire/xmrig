# XMRig

[![Github All Releases](https://img.shields.io/github/downloads/xmrig/xmrig/total.svg)](https://github.com/xmrig/xmrig/releases)
[![GitHub release](https://img.shields.io/github/release/xmrig/xmrig/all.svg)](https://github.com/xmrig/xmrig/releases)
[![GitHub Release Date](https://img.shields.io/github/release-date/xmrig/xmrig.svg)](https://github.com/xmrig/xmrig/releases)
[![GitHub license](https://img.shields.io/github/license/xmrig/xmrig.svg)](https://github.com/xmrig/xmrig/blob/master/LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/xmrig/xmrig.svg)](https://github.com/xmrig/xmrig/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/xmrig/xmrig.svg)](https://github.com/xmrig/xmrig/network)

XMRig is a high performance, open source, cross platform RandomX, KawPow, CryptoNight and [GhostRider](https://github.com/xmrig/xmrig/tree/master/src/crypto/ghostrider#readme) unified CPU/GPU miner and [RandomX benchmark](https://xmrig.com/benchmark). Official binaries are available for Windows, Linux, macOS and FreeBSD.

## Mining backends
- **CPU** (x86/x64/ARMv7/ARMv8/RISC-V)
- **OpenCL** for AMD GPUs.
- **CUDA** for NVIDIA GPUs via external [CUDA plugin](https://github.com/xmrig/xmrig-cuda).

## Download
* **[Binary releases](https://github.com/xmrig/xmrig/releases)**
* **[Build from source](https://xmrig.com/docs/miner/build)**

## Usage
The preferred way to configure the miner is the [JSON config file](https://xmrig.com/docs/miner/config) as it is more flexible and human friendly. The [command line interface](https://xmrig.com/docs/miner/command-line-options) does not cover all features, such as mining profiles for different algorithms. Important options can be changed during runtime without miner restart by editing the config file or executing [API](https://xmrig.com/docs/miner/api) calls.

* **[Wizard](https://xmrig.com/wizard)** helps you create initial configuration for the miner.
* **[Workers](http://workers.xmrig.info)** helps manage your miners via HTTP API.

## Donations
* Default donation 1% (1 minute in 100 minutes) can be increased via option `donate-level` or disabled in source code.
* XMR: `471BVGyBbgFJowPq8fYAyWdomHUmbwY8zQqJGFFtKBeBUdFdCpqnBuB6TxdBZccejNBqLm5PcDBbDbmMsyVhykJxNDKQHe6`

## Developers
* **[xmrig](https://github.com/xmrig)**
* **[sech1](https://github.com/SChernykh)**

## Contacts
* support@xmrig.com
* [reddit](https://www.reddit.com/user/XMRig/)
* [twitter](https://twitter.com/xmrig_dev)

## 如何编译
1. 安装依赖 
brew install cmake libuv openssl hwloc
xcode-select --install
2. 创建build目录 
rm -rf build
mkdir build
cd build
3. cmake
cmake .. -DOPENSSL_ROOT_DIR=$(brew --prefix openssl)
4. 编译
make -j$(sysctl -n hw.logicalcpu)
5. 验证
./xmrig --version

## windows下编译 
1. 下载依赖 
https://github.com/xmrig/xmrig-deps/archive/refs/tags/v25.06.16.zip
2. power shwell执行 
cmake --help | Select-String "Visual Studio"
3. 创建build目录 , 执行如下(把下载的xmrig-deps放到对应的目录)
cmake .. -G "Visual Studio 18 2026" -A x64 -DXMRIG_DEPS=c:\xmrig-deps\msvc2022\x64
4. 成功后再编译
cmake --build . --config Release
5. 生成 文件
build\Release\xmrig.exe

# windows调优
## 调优
根据benchmark来调优
https://xmrig.com/benchmark?cpu=Intel%28R%29+Xeon%28R%29+CPU+E5-2696+v3+%40+2.30GHz
### e5优化
   单cpu可以达9.3kh/s 但是目前开启不了turbo.当前是5.6kh/s
1. 要以管理员运行,不然msr无法打开
2. 开始turbo ,有的华南主板是阉割的, 不能开启.
3. 电源开启高性能
   查看电源计划: powercfg /getactivescheme
   如果不是高性能则设置为高性能: powercfg /setactive SCHEME_MIN
4. 测试 .\xmrig.exe --bench=10M
## linux编译 
1. 下载依赖
apt update

apt install -y \
    git \
    build-essential \
    cmake \
    libuv1-dev \
    libssl-dev \
    libhwloc-dev

2. 编译
mkdir build
cd build
cmake ..
make -j$(nproc)
