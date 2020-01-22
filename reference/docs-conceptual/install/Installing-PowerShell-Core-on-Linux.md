---
title: 在 Linux 上安装 PowerShell Core
description: 介绍如何在各种 Linux 分发上安装 PowerShell Core
ms.date: 07/19/2019
ms.openlocfilehash: 3b0b9b1520247fa49760e631c837196fb7107b5f
ms.sourcegitcommit: cab4e4e67dbed024864887c7f8984abb4db3a78b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/15/2020
ms.locfileid: "76022267"
---
# <a name="installing-powershell-core-on-linux"></a>在 Linux 上安装 PowerShell Core

支持 [Ubuntu 16.04][u16]、[Ubuntu 18.04][u1804]、[Ubuntu 18.10][u1810]、[Ubuntu 19.04][u1904]、[Debian 8][deb8]、[Debian 9][deb9]、[Debian 10][deb10]、[CentOS 7][cos]、[Red Hat Enterprise Linux (RHEL) 7][rhel7]、[openSUSE 42.3][opensuse]、[openSUSE Leap 15][opensuse]、[Fedora 27][fedora]、[Fedora 28][fedora] 和 [Arch Linux][arch]。

对于未获得官方支持的 Linux 分发，可尝试使用 [PowerShell Snap 包][snap]安装 PowerShell。 还可尝试直接使用 Linux [`tar.gz`存档][tar] 部署 PowerShell 二进制文件，但是需要在各个步骤中基于 OS 设置必要的依赖项。

GitHub [版本][]页面上提供有所有可用包。 安装包以后，从终端运行 `pwsh`。 若已安装 [预览版](#installing-preview-releases)，请运行 `pwsh-preview`。

[u16]: #ubuntu-1604
[u1804]: #ubuntu-1804
[u1810]: #ubuntu-1810
[u1904]: #ubuntu-1904
[deb8]: #debian-8
[deb9]: #debian-9
[deb10]: #debian-10
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

> [!TIP]
> 如果已安装 [.NET Core SDK](/dotnet/core/sdk)，则可以轻松地将 PowerShell 作为 [.NET 全局工具](/dotnet/core/tools/global-tools)进行安装。
>
> ```
> dotnet tool install --global PowerShell
> ```

## <a name="installing-preview-releases"></a>安装预览版本

通过包存储库安装适用于 Linux 的 PowerShell Core 预览版本时，包名称从 `powershell` 更改为 `powershell-preview`。

直接下载安装不会更改包名称（文件名除外）。

下表包含使用各种包管理器安装稳定包和预览包的命令：

|分配|稳定包命令 | 预览包命令 |
|---------------|---------------|-----------------|
| Ubuntu、Debian |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| CentOS、RedHat |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| Fedora   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1604"></a>Ubuntu 16.04

### <a name="installation-via-package-repository---ubuntu-1604"></a>通过包存储库安装 - Ubuntu 16.04

为简化安装和更新，已将适用于 Linux 的 PowerShell Core 发布到包存储库。

首选方法如下所示：

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

以超级用户身份注册 Microsoft 存储库一次。 注册后，可以通过 `sudo apt-get upgrade powershell` 更新 PowerShell。

### <a name="installation-via-direct-download---ubuntu-1604"></a>通过直接下载进行安装 - Ubuntu 16.04

从[版本][]页中将 Debian 包 `powershell_7.0.0-1.ubuntu.16.04_amd64.deb` 下载到 Ubuntu 计算机。

然后在终端中执行以下命令：

```sh
sudo dpkg -i powershell_7.0.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` 命令失败，未满足依赖项。 下一命令 `apt-get install -f` 解决此类问题，然后完成 PowerShell 包配置。

### <a name="uninstallation---ubuntu-1604"></a>卸载 - Ubuntu 16.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a>Ubuntu 18.04

### <a name="installation-via-package-repository---ubuntu-1804"></a>通过包存储库安装 - Ubuntu 18.04

为简化安装和更新，已将适用于 Linux 的 PowerShell Core 发布到包存储库。

首选方法如下所示：

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Enable the "universe" repositories
sudo add-apt-repository universe

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

以超级用户身份注册 Microsoft 存储库一次。 注册后，可以通过 `sudo apt-get upgrade powershell` 更新 PowerShell。

### <a name="installation-via-direct-download---ubuntu-1804"></a>通过直接下载安装 - Ubuntu 18.04

从[版本][]页中将 Debian 包 `powershell_7.0.0-1.ubuntu.18.04_amd64.deb` 下载到 Ubuntu 计算机。

然后在终端中执行以下命令：

```sh
sudo dpkg -i powershell_7.0.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` 命令失败，未满足依赖项。 下一命令 `apt-get install -f` 解决此类问题，然后完成 PowerShell 包配置。

### <a name="uninstallation---ubuntu-1804"></a>卸载 - Ubuntu 18.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a>Ubuntu 18.10

安装是通过 `snapd` 受到支持。 有关说明，请参阅 [Snap 包][snap]。

> [!NOTE]
> Ubuntu 18.10 是[支持社区](../powershell-support-lifecycle.md)的[过渡版本](https://www.ubuntu.com/about/release-cycle)。

## <a name="ubuntu-1904"></a>Ubuntu 19.04

安装是通过 `snapd` 受到支持。 有关说明，请参阅 [Snap 包][snap]。

> [!NOTE]
> Ubuntu 19.04 是[社区支持](../powershell-support-lifecycle.md)的[过渡版本](https://www.ubuntu.com/about/release-cycle)。

## <a name="debian-8"></a>Debian 8

### <a name="installation-via-package-repository---debian-8"></a>通过包存储库安装 - Debian 8

为简化安装和更新，已将适用于 Linux 的 PowerShell Core 发布到包存储库。

首选方法如下所示：

```sh
# Install system components
sudo apt-get update
sudo apt-get install -y curl apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

以超级用户身份注册 Microsoft 存储库一次。 注册后，可以通过 `sudo apt-get upgrade powershell` 更新 PowerShell。

## <a name="debian-9"></a>Debian 9

### <a name="installation-via-package-repository---debian-9"></a>通过包存储库安装 - Debian 9

为简化安装和更新，已将适用于 Linux 的 PowerShell Core 发布到包存储库。

首选方法如下所示：

```sh
# Install system components
sudo apt-get update
sudo apt-get install -y curl gnupg apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

以超级用户身份注册 Microsoft 存储库一次。 注册后，可以通过 `sudo apt-get upgrade powershell` 更新 PowerShell。

### <a name="installation-via-direct-download---debian-9"></a>通过直接下载进行安装 - Debian 9

从[版本][]页中将 Debian 包 `powershell_7.0.0-1.debian.9_amd64.deb` 下载到 Debian 计算机。

然后在终端中执行以下命令：

```sh
sudo dpkg -i powershell_7.0.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a>卸载 - Debian 9

```sh
sudo apt-get remove powershell
```

## <a name="debian-10"></a>Debian 10

> [!NOTE]
> Debian 10 仅在 PowerShell 7.0 以及更新版本中受到支持。

### <a name="installation-via-direct-download---debian-10"></a>通过直接下载进行安装 - Debian 10

从[版本][]页中将 tar.gz 包 `powershell_7.0.0-preview-7-linux-x64.tar.gz` 下载到 Debian 计算机。

然后在终端中执行以下命令：

```sh
sudo apt-get update
# install the requirements
sudo apt-get install -y \
        less \
        locales \
        ca-certificates \
        libicu63 \
        libssl1.1 \
        libc6 \
        libgcc1 \
        libgssapi-krb5-2 \
        liblttng-ust0 \
        libstdc++6 \
        zlib1g \
        curl

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v7.0.0-preview.4/powershell-7.0.0-preview.4-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/7-preview

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/7-preview

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/7-preview/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/7-preview/pwsh /usr/bin/pwsh-preview

# Start PowerShell
pwsh-preview
```

## <a name="alpine-39-and-310"></a>Alpine 3.9 和 Alpine 3.10

> [!NOTE]
> Alpine 3.9 和 Alpine 3.10 仅在 PowerShell 7.0 以及更新版本中受到支持。

### <a name="installation-via-direct-download---alpine-39-and-310"></a>通过直接下载进行安装 - Alpine 3.9 和 3.10

从[版本][]页中将 tar.gz 包 `powershell_7.0.0-preview-7-linux-x64.tar.gz` 下载到 Alpine 计算机。

然后在终端中执行以下命令：

```sh
# install the requirements
sudo apk add --no-cache \
    ca-certificates \
    less \
    ncurses-terminfo-base \
    krb5-libs \
    libgcc \
    libintl \
    libssl1.1 \
    libstdc++ \
    tzdata \
    userspace-rcu \
    zlib \
    icu-libs \
    curl

sudo apk -X https://dl-cdn.alpinelinux.org/alpine/edge/main add --no-cache \
    lttng-ust

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v7.0.0-preview.4/powershell-7.0.0-preview.4-linux-alpine-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/7-preview

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/7-preview

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/7-preview/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/7-preview/pwsh /usr/bin/pwsh-preview

# Start PowerShell
pwsh-preview
```

## <a name="centos-7"></a>CentOS 7

> [!NOTE]
> 此包可以在 Oracle Linux 7 上运行。

### <a name="installation-via-package-repository-preferred---centos-7"></a>通过包存储库安装（首选）- CentOS 7

为简化安装和更新，已将适用于 Linux 的 PowerShell Core 发布到正式的 Microsoft 存储库。

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

以超级用户身份注册 Microsoft 存储库一次。 注册后，可以通过 `sudo yum update powershell` 更新 PowerShell。

### <a name="installation-via-direct-download---centos-7"></a>通过直接下载进行安装 - CentOS 7

使用 [CentOS 7][]时，请从[版本][]页中将 RPM 包 `powershell-7.0.0-1.rhel.7.x86_64.rpm` 下载到 CentOS 计算机。

然后在终端中执行以下命令：

```sh
sudo yum install powershell-7.0.0-1.rhel.7.x86_64.rpm
```

无需该中间下载步骤即可安装 RPM：

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v7.0.0/powershell-7.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a>卸载 - CentOS 7

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a>Red Hat Enterprise Linux (RHEL) 7

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a>通过包存储库安装（首选）- Red Hat Enterprise Linux (RHEL) 7

为简化安装和更新，已将适用于 Linux 的 PowerShell Core 发布到正式的 Microsoft 存储库。

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

以超级用户身份注册 Microsoft 存储库一次。 注册后，可以通过 `sudo yum update powershell` 更新 PowerShell。

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a>通过直接下载进行安装 - Red Hat Enterprise Linux (RHEL) 7

从[版本][]页中将 RPM 包 `powershell-7.0.0-1.rhel.7.x86_64.rpm` 下载到 Red Hat Enterprise Linux 计算机。

然后在终端中执行以下命令：

```sh
sudo yum install powershell-7.0.0-1.rhel.7.x86_64.rpm
```

无需该中间下载步骤即可安装 RPM：

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v7.0.0/powershell-7.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a>卸载 - Red Hat Enterprise Linux (RHEL) 7

```sh
sudo yum remove powershell
```

## <a name="opensuse"></a>OpenSUSE

### <a name="installation---opensuse-423"></a>安装 - openSUSE 42.3

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar libicu52_1

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v7.0.0/powershell-7.0.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/7

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/7

# Set execute permissions
chmod +x /opt/microsoft/powershell/7/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/7/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="installation---opensuse-leap-15"></a>安装 - openSUSE Leap 15

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar gzip libopenssl1_0_0 libicu60_2

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v7.0.0/powershell-7.0.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/7

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/7

# Set execute permissions
chmod +x /opt/microsoft/powershell/7/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/7/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="uninstallation---opensuse-423-opensuse-leap-15"></a>卸载 - OpenSUSE 42.3、openSUSE Leap 15

```sh
rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="fedora"></a>Fedora

> [!NOTE]
> Fedora 28 仅在 PowerShell Core 6.1 以及更新版本中受到支持。

> [!NOTE]
> Fedora 29 和 Fedora 30 仅在 PowerShell 7.0 以及更新版本中受到支持。

### <a name="installation-via-package-repository-preferred---fedora-28-29-and-30"></a>通过包存储库安装（首选）- Fedora 28、Fedora 29 和 Fedora 30

为简化安装和更新，已将适用于 Linux 的 PowerShell Core 发布到正式的 Microsoft 存储库。

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install a system component
sudo dnf install compat-openssl10

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-28-29-and-30"></a>通过直接下载进行安装 - Fedora 28、Fedora 29 和 Fedora 30

从[版本][]页中将 RPM 包 `powershell-7.0.0-1.rhel.7.x86_64.rpm` 下载到 Fedora 计算机。

然后在终端中执行以下命令：

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-7.0.0-1.rhel.7.x86_64.rpm
```

无需该中间下载步骤即可安装 RPM：

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v7.0.0/powershell-7.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-28-29-and-30"></a>卸载 - Fedora 28、Fedora 29 和 Fedora 30

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a>Arch Linux

> [!NOTE]
> Arch 支持不受 Microsoft 的官方支持且由社区维护。

[Arch Linux][] 用户存储库 (AUR) 中提供有 PowerShell。

* 可使用[最新标记版本][arch-release]对其进行编译
* 可使用[最新 commit to master][arch-git] 对其进行编译
* 可使用[最新版本二进制文件][arch-bin]进行安装

AUR 中的包由社区维护，并无正式支持。

有关从 AUR 安装包的详细信息，请参阅 [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) 或 [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile) 社区。

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a>Snap 包

### <a name="getting-snapd"></a>获取 snapd

需具备 `snapd` 才能运行 Snap。 按照[这些说明](https://docs.snapcraft.io/core/install)确保你已安装 `snapd`。

### <a name="installation-via-snap"></a>通过 Snap 进行安装

为简化安装和更新，已向 [Snap 存储](https://snapcraft.io/store)发布 PowerShell Core for Linux。

首选方法如下所示：

```sh
# Install PowerShell
sudo snap install powershell --classic

# Start PowerShell
pwsh
```

若要安装预览版本，请使用以下方法：

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

安装完成后，Snap 将自动升级。 可以使用 `sudo snap refresh powershell` 或 `sudo snap refresh powershell-preview` 触发升级。

### <a name="uninstallation"></a>卸载

```sh
sudo snap remove powershell
```

或

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a>Kali

> [!NOTE]
> Kali 支持不受 Microsoft 的官方支持且由社区维护。

### <a name="installation---kali"></a>安装 - Kali

```sh
# Install PowerShell package
apt update && apt -y install powershell

# Start PowerShell
pwsh
```

### <a name="uninstallation---kali"></a>卸载 - Kali

```sh
# Uninstall PowerShell package
apt -y remove powershell
```

## <a name="raspbian"></a>Raspbian

> [!NOTE]
> Raspbian 支持是实验性的。

当前仅 Raspbian Stretch 支持 PowerShell。

CoreCLR 和 PowerShell Core 仅适用于 Pi 2 和 Pi 3 设备，因为其他设备（如 [Pi 0](https://github.com/dotnet/coreclr/issues/10605)）有不受支持的处理器。

下载 [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) 并按照[安装说明](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)操作，将其安装在你的 Pi 上。

### <a name="installation---raspbian"></a>安装 - Raspbian

```sh
###################################
# Prerequisites

# Update package lists
sudo apt-get update

# Install libunwind8 and libssl1.0
# Regex is used to ensure that we do not install libssl1.0-dev, as it is a variant that is not required
sudo apt-get install '^libssl1.0.[0-9]$' libunwind8 -y

###################################
# Download and extract PowerShell

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v7.0.0/powershell-7.0.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-7.0.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

或者，可以创建可启动 PowerShell 的符号链接，而无需指定到 `pwsh` 二进制文件的路径。

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a>卸载 - Raspbian

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a>二进制存档

已对 Linux 平台提供 PowerShell 二进制 `tar.gz` 存档，以启用高级部署方案。

### <a name="dependencies"></a>依赖项

PowerShell 为所有 Linux 分发版生成可移植二进制文件。 但是对于不同的分发版，.NET Core 运行时需要不同的依赖项，并且 PowerShell 也有相同要求。

下表列出了在不同 Linux 分发版上正式支持的 .NET Core 2.0 依赖项。

| OS                 | 依赖项 |
| ------------------ | ------------ |
| Ubuntu 16.04       | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.0、libicu55 |
| Ubuntu 17.10       | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.0、libicu57 |
| Ubuntu 18.04       | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.0、libicu60 |
| Debian 8 (Jessie)  | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.0、libicu52 |
| Debian 9 (Stretch) | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.2、libicu57 |
| CentOS 7 <br> Oracle Linux 7 <br> RHEL 7 | libunwind、libcurl、openssl-libs、libicu |
| openSUSE 42.3 | libcurl4、libopenssl1_0_0、libicu52_1 |
| openSUSE Leap 15 | libcurl4、libopenssl1_0_0、libicu60_2 |
| Fedora 27 <br> Fedora 28 | libunwind、libcurl、openssl-libs、libicu、compat-openssl10 |

若要在不受正式支持的 Linux 分发版上部署 PowerShell 二进制文件，则需在各个步骤中安装目标 OS 的必要依赖项。 例如，[Amazon Linux dockerfile][amazon-dockerfile] 先安装依赖项，然后提取 Linux `tar.gz` 存档。

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell-Docker/blob/master/release/community-stable/amazonlinux/docker/Dockerfile

### <a name="installation---binary-archives"></a>安装 - 二进制存档

#### <a name="linux"></a>Linux

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v7.0.0/powershell-7.0.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/7

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/7

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/7/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/7/pwsh /usr/bin/pwsh
```

### <a name="uninstalling-binary-archives"></a>卸载二进制存档

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a>路径

* `$PSHOME` 是 `/opt/microsoft/powershell/7/`
* 将从 `~/.config/powershell/profile.ps1` 中读取用户配置文件
* 将从 `$PSHOME/profile.ps1` 中读取默认配置文件
* 将从 `~/.local/share/powershell/Modules` 中读取用户模块
* 将从 `/usr/local/share/powershell/Modules` 中读取共享模块
* 将从 `$PSHOME/Modules` 中读取默认模块
* PSReadline 历史记录将记录到 `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

配置文件采用 PowerShell 的按主机配置，所以默认主机特定配置文件位于相同位置下的 `Microsoft.PowerShell_profile.ps1` 中。

PowerShell 采用 Linux 上的 [XDG 基目录规范][xdg-bds]。

[版本]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
