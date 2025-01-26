# 开发环境搭建指南

## 一、安装必要工具

在开始搭建开发环境之前，我们需要安装一系列必要的工具。打开终端，执行以下命令：

```shell
sudo apt-get install git wget flex bison gperf python3 python3-pip python3-venv cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0
```

## 二、克隆 esp-idf 仓库

### 2.1 创建工作目录并克隆仓库

首先，创建一个专门用于存放 `esp-idf` 项目的目录，然后进入该目录并从 Github 克隆 `esp-idf` 仓库：

```bash
mkdir -p ~/esp
cd ~/esp
git clone --recursive https://github.com/espressif/esp-idf.git
```

`--recursive` 参数的作用是在克隆主仓库的同时，递归克隆所有子模块，确保项目的完整性。

### 2.2 下载 esp-gitee-tools 工具

为了能够克隆子仓库并安装工具链，我们需要使用 `esp-gitee-tools` 工具。进入 `esp-idf` 目录并从 Gitee 克隆该工具：

```bash
cd ~/esp/esp-idf
git clone https://gitee.com/EspressifSystems/esp-gitee-tools.git
```

### 2.3 克隆子模块

进入 `esp-idf` 目录，执行脚本以克隆子模块：

```bash
cd ~/esp/esp-idf
./esp-gitee-tools/submodule-update.sh
```

该脚本会帮助我们完成子模块的克隆工作，保证项目的所有依赖都被正确获取。

## 三、安装工具链

安装工具链所需的工具包较多，整个过程大约需要 10 分钟。在 `esp-idf` 目录下执行安装脚本：

```bash
cd ~/esp/esp-idf
./esp-gitee-tools/install.sh
```

## 四、激活 esp-idf

### 4.1 配置环境变量别名

为了方便激活 `esp-idf` 环境，我们在 `~/.bashrc` 文件中添加一行命令，设置一个别名：

# 验证esp-idf

```bash
echo "alias get_idf='. ~/esp/esp-idf/export.sh'" >> ~/.bashrc
```

这行命令会将 `get_idf` 定义为激活 `esp-idf` 环境的快捷命令。

### 4.2 激活配置文件

执行以下命令使 `~/.bashrc` 文件的修改生效：

```bash
source ~/.bashrc
```

之后，在任何终端窗口中，只需执行 `get_idf` 命令，即可激活 `esp-idf` 环境。

## 五、验证 esp-idf

### 5.1 复制示例项目

创建一个用于存放示例项目的目录，并将 `esp-idf` 中的示例项目复制到该目录：

```shell
cd ~/esp
mkdir app-example
cp -r esp-idf/examples/* app-example/
```

### 5.2 进入示例项目目录

进入 `blink` 示例项目的目录：

```bash
cd app-example/get-started/blink/
```

### 5.3 安装 ninja 及其依赖

#### 5.3.1 安装依赖 re2c

执行以下命令安装 `re2c` 依赖：

```bash
sudo apt install re2c
```

#### 5.3.2 验证 re2c 安装

使用以下命令验证 `re2c` 是否安装成功：

```bash
re2c --version
```

#### 5.3.3 下载 ninja 源码

从 Github 克隆 `ninja` 的源码仓库：

```bash
git clone https://github.com/ninja-build/ninja.git
```

#### 5.3.4 编译并安装 ninja

进入 `ninja` 目录，执行编译脚本并将编译好的 `ninja` 可执行文件复制到系统路径：

```bash
cd ./ninja
./configure.py --bootstrap
sudo cp ./ninja /usr/bin
```

#### 5.3.5 验证 ninja 安装

使用以下命令验证 `ninja` 是否安装成功：

### 验证ninja

```bash
ninja --version
```

## 六、配置 SSH 免登录（Windows 系统）

### 6.1 生成 SSH 密钥

在 Windows 上打开 PowerShell，输入以下命令生成 SSH 密钥：

在Windows上打开powershell，输入

```shell
ssh-keygen -t ed25519 -C "vi2@gitee.com"
```

然后一路回车，接受默认设置。

### 6.2 复制公钥内容

打开 `C:\Users\Administrator.ssh` 目录，找到 `id_ed25519.pub` 文件，复制其内容。

### 6.3 添加公钥到授权文件

将复制的公钥内容添加到 `~/.ssh/authorized_keys` 文件中，这样就可以实现 SSH 免登录。
