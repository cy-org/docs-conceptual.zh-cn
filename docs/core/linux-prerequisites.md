---
title: "Linux 上 .NET Core 的先决条件"
description: "支持的 Linux 版本和 .NET Core 依赖项，用于在 Linux 计算机上开发、部署和运行 .NET Core 应用程序。"
keywords: .NET, .NET Core, Linux, debian, ubuntu, RHEL, centOS,
author: jralexander
ms.author: johalex
ms.date: 09/07/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
ms.translationtype: HT
ms.sourcegitcommit: 1b0379156f44b0a3e765f8d832c7a1ca74ee3598
ms.openlocfilehash: d9da6ea27293e95e36ff8edc42ef8bafbc86c8ec
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---

# <a name="prerequisites-for-net-core-on-linux"></a>Linux 上 .NET Core 的先决条件

本文介绍了在 Linux 上开发 .NET Core 应用程序所需的依赖项。 支持的 Linux 发行版本/版本和依赖项适用于在 Linux 上开发 .NET Core 应用程序的两种方法：

* [结合使用命令行和常用编辑器](tutorials/using-with-xplat-cli.md)
* [Visual Studio Code](https://code.visualstudio.com/)

## <a name="supported-linux-versions"></a>支持的 Linux 版本

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

.NET Core 2.0 将 Linux 视为一个操作系统。 支持的 Linux 发行版本都对应有一个 Linux 版本（每芯片体系结构）。

以下 Linux 64 位（`x86_64` 或 `amd64`）发行版本/版本支持 NET Core 2.x：

 * Red Hat Enterprise Linux 7
 * CentOS 7
 * Oracle Linux 7
 * Fedora 25、Fedora 26
 * Debian 8.7 或更高版本 
 * Ubuntu 17.04、Ubuntu 16.04、Ubuntu 14.04
 * Linux Mint 18、Linux Mint 17
 * openSUSE 42.2 或更高版本
 * SUSE Enterprise Linux (SLES) 12 SP2 或更高版本

有关支持 .NET Core 2.x 的操作系统、不支持的 OS 版本和生命周期策略链接的完整列表，请参阅 [.NET Core 2.x - 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/2.0/2.0-supported-os.md)。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

以下 Linux 64 位（`x86_64` 或 `amd64`）发行版本/版本支持 .NET Core 1.x：

* Red Hat Enterprise Linux 7
* CentOS 7
* Oracle Linux 7
* Fedora 24
* Debian 8.2 或更高版本
* Ubuntu 14.04、Ubuntu 16.04、Ubuntu 16.10\*
 * 最新修补版 .NET Core 1.1 支持 Ubuntu 16.10
* Linux Mint 17
* openSUSE 42.1 或更高版本 (.NET Core 1.1)

有关支持 .NET Core 1.x 的操作系统、不支持的 OS 版本和生命周期策略链接的完整列表，请参阅 [.NET Core 1.x - 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0-supported-os.md)。

---

## <a name="linux-distribution-dependencies"></a>Linux 发行版本依赖项

### <a name="ubuntu"></a>Ubuntu

Ubuntu 发行版本需要安装以下库：

* libunwind8
* libunwind8-dev
* gettext
* libicu-dev
* liblttng-ust-dev
* libcurl4-openssl-dev
* libssl-dev
* uuid-dev
* unzip

### <a name="centos"></a>CentOS

CentOS 发行版本需要安装以下库：

* deltarpm
* epel-release
* unzip
* libunwind
* gettext
* libcurl-devel
* openssl-devel
* zlib
* libicu-devel

有关依赖项的详细信息，请参阅[独立式 Linux 应用程序](https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md)。

## <a name="installing-net-core-dependencies-with-the-native-installers"></a>使用本机安装程序安装 .NET Core 依赖项

.NET Core 本机安装程序适用于支持的 Linux 发行版本/版本。 本机安装程序需要拥有对服务器的管理员 (sudo) 访问权限。 使用本机安装程序的优势在于，可以安装所有 .NET Core 本机依赖项。 本机安装程序还会在整个系统内安装 .NET Core SDK。

在 Linux 上，安装程序包有两种使用方式：

* 使用基于源的包管理器，如适用于 Ubuntu 的 apt-get，或适用于 CentOS/RHEL 的 yum。
* 使用包本身（DEB 或 RPM）。

### <a name="scripting-installs-with-the-net-core-installer-script"></a>使用 .NET Core 安装程序脚本编写安装脚本

`dotnet-install` 脚本用于执行 CLI 工具链和共享运行时的非管理员安装。 可以从 [CLI GitHub 存储库](https://github.com/dotnet/cli/tree/rel/1.0.0/scripts/obtain)下载脚本。

安装程序 bash 脚本用于自动化方案和非管理员安装。 此脚本也读取 PowerShell 开关，因此可以与 Linux/OS X 系统上的脚本结合使用。

> [!IMPORTANT]
> 运行脚本前，请安装所需的[依赖项](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)。

## <a name="install-net-core-for-red-hat-enterprise-linux-rhel-7"></a>为 Red Hat Enterprise Linux (RHEL) 7 安装 .NET Core

在 RHEL 7 上安装 .NET Core：

1. 启用 Red Hat .NET 通道（在 RHEL 7 订阅下）。
    * 对于 Red Hat Enterprise 7 服务器，请使用：
    
         ```bash
         subscription-manager repos --enable=rhel-7-server-dotnet-rpms
         ```
    
    * 对于 Red Hat Enterprise 7 工作站，请使用：
    
        ```bash
        subscription-manager repos --enable=rhel-7-workstation-dotnet-rpms
         ```
    
    * 对于 Red Hat Enterprise 7 HPC 计算节点，请使用：
    
        ```bash
        subscription-manager repos --enable=rhel-7-hpc-node-dotnet-rpms
        ```

2. 安装 scl 工具。

    ```bash
    yum install scl-utils
    ```
    
3. 安装 .NET Core

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

安装 .NET Core 2.0 SDK 和运行时：

   ```bash
   yum install rh-dotnet20
   ```

为环境启用 .NET Core 2.0 SDK/运行时：

   ```bash
   scl enable rh-dotnet20 bash
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

**.NET Core 1.1**

安装 .NET Core 1.1 SDK 和运行时：

   ```bash
   yum install rh-dotnetcore11
   ```

为环境启用 .NET Core 1.1 SDK 和运行时：

   ```bash
   scl enable rh-dotnetcore11 bash
   ```

**.NET Core 1.0**

安装 .NET Core 1.0 SDK 和运行时：

   ```bash
   yum install rh-dotnetcore10
   ```

为环境启用 .NET Core 1.0 SDK 和运行时：

   ```bash
   scl enable rh-dotnetcore10 bash
   ```

---
4. 运行 `dotnet --version` 命令，以证明安装成功。

     ```bash
     dotnet --version
     ```

若要获取 Red Hat .NET 通道访问注册方面的帮助，请参阅 Red Hat 提供的 [.NET Core 1.1 入门指南的第 1 章](https://access.redhat.com/documentation/en/net-core/1.1/paged/getting-started-guide/)。

## <a name="install-net-core-for-ubuntu-1404-ubuntu-1604-ubuntu-1610--linux-mint-17-linux-mint-18-64-bit"></a>为 Ubuntu 14.04、Ubuntu 16.04、Ubuntu 16.10、Linux Mint 17 和 Linux Mint 18（64 位）安装 .NET Core

1. 从系统中删除 .NET Core 的所有旧预览版本。

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

2. 注册受信任的 Microsoft 产品密钥。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
   ```

3. 设置所需的版本宿主包源。

   **Ubuntu 17.04**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-zesty-prod zesty main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-get update
   ```

   **Ubuntu 16.04 / Linux Mint 18**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-xenial-prod xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-get update
   ```

   **Ubuntu 14.04 / Linux Mint 17**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-trusty-prod trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-get update
   ```

4. 安装 .NET Core。

   ```bash
   sudo apt-get install dotnet-sdk-2.0.0
   ```

4. 运行 `dotnet --version` 命令，以证明安装成功。

   ```bash
   dotnet --version
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

2. 设置所需的版本宿主包源。

   **Ubuntu 16.10**
   
   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B02C46DF417A0893
   sudo apt-get update
   ```

  **Ubuntu 16.04 / Linux Mint 18**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B02C46DF417A0893
   sudo apt-get update
   ```
    
   **Ubuntu 14.04 / Linux Mint 17**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B02C46DF417A0893
   sudo apt-get update
   ```

3. 在 Ubuntu 或 Linux Mint 上安装 .NET Core 1.x：

   ```bash
   sudo apt-get install dotnet-dev-1.0.4
   ```

4. 运行 `dotnet --version` 命令，以证明安装成功。

   ```bash
   dotnet --version
   ```

---

 ## <a name="install-net-core-for-debian-8-or-debian-9-64-bit"></a>为 Debian 8 或 Debian 9（64 位）安装 .NET Core

在 Debian 8 或 Debian 9（64 位）上安装 .NET Core 的具体步骤：

1. 从系统中删除 .NET Core 的所有旧预览版本。

> [!NOTE]
> 必须有用户控制目录，才能通过 tar.gz 在 Linux 系统上进行安装。

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

2. 安装系统组件。

   ```bash
   sudo apt-get update
   sudo apt-get install curl libunwind8 gettext apt-transport-https
   ```
   
3. 注册受信任的 Microsoft 产品密钥。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
   ```
   
4. 注册 Microsoft 产品源。

   **Debian 9 (Stretch)**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/dotnetdev.list'
   ```
   
   **Debian 8 (Jessie)**
   
   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main" > /etc/apt/sources.list.d/dotnetdev.list'
   ```
   
5. 安装 .NET Core SDK。

   ```bash
   sudo apt-get update
   sudo apt-get install dotnet-sdk-2.0.0
   ```

6. 将 dotnet 添加到 PATH。

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```
   
7. 运行 `dotnet --version` 命令，以证明安装成功。

   ```bash
   dotnet --version
   ```   
  

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

2. 获取系统必备。

   ```bash
   sudo apt-get install curl libunwind8 gettext
   ```

3. 下载 .NET Core SDK 二进制文件 (tarball)。

   ```bash
   curl -sSL -o dotnet.tar.gz https://go.microsoft.com/fwlink/?linkid=848826
   ```

4. 提取 .NET Core SDK 二进制文件。

   ```bash
   sudo mkdir -p /opt/dotnet && sudo tar zxf dotnet.tar.gz -C /opt/dotnet
   ```

5. 将 dotnet 添加到 PATH。

   ```bash
   sudo ln -s /opt/dotnet/dotnet /usr/local/bin
   ```

6. 运行 `dotnet --version` 命令，以证明安装成功。

   ```bash
   dotnet --version
   ```

---

## <a name="install-net-core-for-fedora-24-fedora-25-or-fedora-26-64-bit"></a>为 Fedora 24、Fedora 25 或 Fedora 26（64 位）安装 .NET Core

若要在 Fedora 26 或 Fedora 25 上安装 .NET Core 2.x，或在 Fedora 24 上安装 .NET Core 1.x，请执行以下操作：

1. 从系统中删除 .NET Core 的所有旧预览版本。

> [!NOTE]
> 必须有用户控制目录，才能通过 tar.gz 在 Linux 系统上进行安装。

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

**Fedora 26 或 Fedora 25**

2. 注册 Microsoft 签名密钥。

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

3. 添加 dotnet 产品源。

   ```bash
   sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl=https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/dotnetdev.repo'
   ```

4. 安装 .NET Core SDK。

   ```bash
   sudo dnf update
   sudo dnf install libunwind libicu
   sudo dnf install dotnet-sdk-2.0.0
   ```

5. 将 dotnet 添加到 PATH。

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

**Fedora 24**

2. 获取系统必备。

   ```bash
   sudo dnf install libunwind libicu
   ```

3. 下载 .NET Core SDK 二进制文件 (tarball)。

   ```bash
   curl -sSL -o dotnet.tar.gz https://go.microsoft.com/fwlink/?linkid=848833
   ```

4. 提取 .NET Core SDK 二进制文件。

   ```bash
   sudo mkdir -p /opt/dotnet && sudo tar zxf dotnet.tar.gz -C /opt/dotnet
   ```

5. 将 dotnet 添加到 PATH。

   ```bash
   sudo ln -s /opt/dotnet/dotnet /usr/local/bin
   ```
   
---

6. 运行 `dotnet --version` 命令，以证明安装成功。

   ```bash
   dotnet --version
   ```

## <a name="install-net-core-for-centos-71-64-bit--oracle-linux-71-64-bit"></a>为 CentOS 7.1（64 位）和 Oracle Linux 7.1（64 位）安装 .NET Core

若要为 CentOS 7.1（64 位）和 Oracle Linux 7.1（64 位）安装 .NET Core，请执行以下操作：

1. 从系统中删除 .NET Core 的所有旧预览版本。

> [!NOTE]
> 必须有用户控制目录，才能通过 tar.gz 在 Linux 系统上进行安装。

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

2. 注册 Microsoft 签名密钥。

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

3. 添加 Microsoft 产品源。

   ```bash
   sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl=https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/dotnetdev.repo'
   ```

4. 安装 .NET Core SDK。

   ```bash
   sudo yum update
   sudo yum install libunwind libicu
   sudo yum install dotnet-sdk-2.0.0
   ```

5. 将 dotnet 添加到 PATH

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

2. 获取系统必备。

   ```bash
   sudo yum install libunwind libicu
   ```
   
3. 下载 .NET Core SDK 二进制文件 (tarball)。

   ```bash
   curl -sSL -o dotnet.tar.gz https://go.microsoft.com/fwlink/?linkid=848821
   ```

4. 提取 .NET Core SDK 二进制文件。

   ```bash
   sudo mkdir -p /opt/dotnet && sudo tar zxf dotnet.tar.gz -C /opt/dotnet
   ```

5. 将 dotnet 添加到 PATH。

   ```bash
   sudo ln -s /opt/dotnet/dotnet /usr/local/bin
   ```

---

6. 运行 `dotnet --version` 命令，以证明安装成功。

   ```bash
   dotnet --version
   ```

## <a name="install-net-core-for-suse-linux-enterprise-server-64-bit"></a>为 SUSE Linux Enterprise Server（64 位）安装 .NET Core

若要为 SUSE Linux Enterprise Server (SLES) 12 SP2（64 位）安装 .NET Core 2.x，请执行以下操作：

1. 从系统中删除 .NET Core 的所有旧预览版本。

2. 添加 dotnet 产品源。

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl=https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/dotnetdev.repo'
   ```

3. 安装 .NET Core SDK。

   ```bash
   sudo zypper update
   sudo zypper install libunwind libicu
   sudo zypper install dotnet-sdk-2.0.0
   ```

4. 将 dotnet 添加到 PATH。

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```

5. 运行 `dotnet --version` 命令，以证明安装成功。

   ```bash
   dotnet --version
   ```
   
## <a name="install-net-core-for-opensuse-64-bit"></a>为 openSUSE（64 位）安装 .NET Core

若要为 openSUSE 安装 .NET Core 2.x 或者为 openSUSE（64 位）安装 .NET Core 1.x，请执行以下操作：

1. 从系统中删除 .NET Core 的所有旧预览版本。

> [!NOTE]
> 必须有用户控制目录，才能通过 tar.gz 在 Linux 系统上进行安装。

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

2. 注册 Microsoft 签名密钥。

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

3. 添加 dotnet 产品源。

   ```bash
   sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl=https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/dotnetdev.repo'
   ``` 

4. 安装 .NET Core SDK。

   ```bash
   sudo zypper update
   sudo zypper install libunwind libicu
   sudo zypper install dotnet-sdk-2.0.0
   ```

5. 将 dotnet 添加到 PATH。

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

2. 获取系统必备。

   ```bash
   sudo zypper install libunwind libicu
   ```

3. 下载 .NET Core SDK 二进制文件 (tarball)。

   ```bash
   curl -sSL -o dotnet.tar.gz https://go.microsoft.com/fwlink/?linkid=848824
   ```

4. 提取 .NET Core SDK 二进制文件。
   
   ```bash
   sudo mkdir -p /opt/dotnet && sudo tar zxf dotnet.tar.gz -C /opt/dotnet
   ```

5. 将 dotnet 添加到 PATH。

   ```bash
   sudo ln -s /opt/dotnet/dotnet /usr/local/bin
   ```
   
---

6. 运行 `dotnet --version` 命令，以证明安装成功。

   ```bash
   dotnet --version
   ```

> [!IMPORTANT]
> 若对在支持的 Linux 发行版本/版本上安装 .NET Core 2.x 有疑问，请参阅每个已安装的发行版本/版本对应的 [2.0 已知问题](https://github.com/dotnet/core/tree/master/release-notes/2.0)主题。 
>
> 若对在支持的 Linux 发行版本/版本上安装 .NET Core 1.x 有疑问，请参阅每个已安装的发行版本/版本对应的 [1.0.0 已知问题](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0-known-issues.md)和 [1.0.1 已知问题](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.1-known-issues.md)主题。

