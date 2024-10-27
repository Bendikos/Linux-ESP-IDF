# 安装各种必要的工具

```shell
sudo apt-get install git wget flex bison gperf python3\
 python3-pip python3-venv cmake ninja-build ccache\
 libffi-dev libssl-dev dfu-util libusb-1.0-0
```

# 从Gitee克隆esp-idf仓库

```shell
mkdir -p ~/esp
cd ~/esp
git clone --recursive https://github.com/espressif/esp-idf.git
```

# 为了克隆子仓库和安装工具链

需要用到esp-gitee-tools工具，下载该工具到本地。

```shell
cd ~/esp/esp-idf
git clone https://gitee.com/EspressifSystems/esp-gitee-tools.git
```

# 克隆子模块

```shell
cd ~/esp/esp-idf
./esp-gitee-tools/submodule-update.sh
```

# 安装工具链

需要下载的工具包比较多，大约需要10分钟左右

```shell
cd ~/esp/esp-idf
./esp-gitee-tools/install.sh
```

# 激活esp-idf

在 ~/.bashrc 文件中增加 一行命令：`alias get_idf='. ~/esp/esp-idf/export.sh'`

执行命令：`source ~/.bashrc` 激活该文件。 在任何Terminal窗口均可以执行命令：`get_idf`，激活esp-idf环境。

# 验证esp-idf

```shell
cd ~/esp
mkdir app-example
cp -r  esp-idf/examples/* app-example/
cd app-example/get-started/blink/

```

# 可能需要

## ninja的安装

### 安装依赖`re2c`。

```shell
sudo apt install re2c
```

### 验证依赖`re2c`

```shell
re2c --version
```

### 下载ninja的源码

```shell
git clone https://github.com/ninja-build/ninja.git
```

### 进入刚才下载的ninja目录中，执行编译脚本。

```shell
cd ./ninja
./configure.py --bootstrap
```

### 安装ninja

```shell
sudo cp ./ninja /usr/bin
```

### 验证ninja

```shell
ninja --version
```

