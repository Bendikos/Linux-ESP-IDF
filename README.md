## 安装esp-idf

### 1、安装各种必要的工具

```shell
sudo apt-get install git wget flex bison gperf python3-pip python3-venv cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0 net-tools
```

### 2、新建esp32目录

```shell
mkdir esp32
cd esp32
```

### 3、拉取gitee工具

```shell
git clone https://gitee.com/EspressifSystems/esp-gitee-tools.git
```

### 4、执行gitee工具切换镜像脚本

```shell
cd esp-gitee-tools
./jihu-mirror.sh set
```

### 5、拉取esp-idf源码

```shell
cd ..
git clone --recursive https://github.com/espressif/esp-idf.git
```

### 6、切换esp-idf版本分支到v5.2

```shell
cd esp-idf
git checkout v5.2
```


### 验证esp-idf分支是否切换

```shell
git branch
```

### 初始化esp-idfv5.2

```shell
git submodule update --init --recursive
如果提示失败或有错误试下这句：../esp-gitee-tools/submodule-update.sh
```

### 7、更换pip源

```shell
pip config set global.index-url http://mirrors.aliyun.com/pypi/simple
pip config set global.trusted-host mirrors.aliyun.com
```

### 8、安装编译工具

```shell
../esp-gitee-tools/install.sh
```

### 9、设置环境变量

```shell
source export.sh
```

```shell
vim /home/zuozhongkai/.profile
```

输入以下代码

```tex
source ~/esp32/esp-idf/export.sh
```

### 10、下载课程配套源码

```shell
cd ~/esp32
git clone --recursive https://gitee.com/vi-iot/esp32-board.git
```

### 11、验证esp-idf

```shell
cd esp32-board/helloworld
idf.py build
```

### 12、设置USB串口权限

```shell
sudo usermod -aG dialout zuozhongkai
```

### 13、重启Ubuntu











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

