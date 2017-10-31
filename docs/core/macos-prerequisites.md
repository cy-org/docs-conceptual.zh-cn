---
title: "Mac 上 .NET Core 的先决条件"
description: "在 macOS 计算机上开发、部署和运行 .NET Core 应用程序所支持的 macOS 版本和 .NET Core 依赖项。"
keywords: .NET, .NET Core, macOS, Mac
author: guardrex
ms.author: mairaw
ms.date: 07/07/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8feaee2cbfa55e23bd49c0ab76d995f15be343b4
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="prerequisites-for-net-core-on-mac"></a>Mac 上 .NET Core 的先决条件

本文介绍了在 macOS 计算机上开发、部署和运行 .NET Core 应用程序所需的受支持的 macOS 版本和 .NET Core 依赖项。 支持的操作系统版本和随附的依赖项适用于在 Mac 上开发 .NET Core 应用的三种方法：[结合使用常用编辑器和命令行](tutorials/using-with-xplat-cli.md)、[Visual Studio Code](https://code.visualstudio.com/) 和 [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/)。

## <a name="supported-macos-versions"></a>支持的 macOS 版本

以下 macOS 版本均支持 .NET Core：

* macOS 10.12“Sierra”
* macOS 10.11“El Capitan”（仅支持 .NET Core 1.x）

在[支持的操作系统版本](https://github.com/dotnet/core/blob/master/roadmap.md#supported-os-versions)中查看受支持的操作系统的完整列表。

## <a name="net-core-dependencies"></a>.NET Core 依赖项

**.NET Core 1.x**

在 macOS 上运行时，.NET Core 1.x 需要 OpenSSL。 获取 OpenSSL 的一个简单方法是使用适用于 macOS 的 [Homebrew (“brew”)](https://brew.sh/) 包。 在安装 *brew* 后，通过在终端（命令）提示符处执行以下命令来安装 OpenSSL：

```console
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

从 [.NET 下载](https://www.microsoft.com/net/download/core)下载并安装 .NET Core SDK。 如果在 macOS 上安装时遇到问题，请查阅 [1.0.0 已知问题](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0-known-issues.md)和 [1.0.1 已知问题](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.1-known-issues.md)主题。

**.NET Core 2.x**

从 [.NET 下载](https://www.microsoft.com/net/download/core)下载并安装 .NET Core SDK。 如果在 macOS 上安装时遇到问题，请查阅适用于已安装的版本的[已知问题](https://github.com/dotnet/core/tree/master/release-notes/2.0)主题。

## <a name="visual-studio-for-mac"></a>Visual Studio for Mac

可以使用任何编辑器，通过 .NET Core SDK 开发 .NET Core 应用程序。 但是，若要在集成的开发环境中的 Mac 上开发 .NET Core 应用程序，可以使用 [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/)。 

使用 Visual Studio for Mac 在 macOS 上进行 .NET Core 开发需要：

* macOS 操作系统的受支持版本
* OpenSSL（仅 .NET Core 1.x；.NET Core 2.x 使用 macOS 上本机可用的安全服务）
* .NET Core SDK for Mac
* [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/)

