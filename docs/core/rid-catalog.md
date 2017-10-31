---
title: ".NET Core 运行时标识符 (RID) 目录"
description: "了解运行时标识符 (RID) 及如何在 .NET Core 中使用 RID。"
author: mairaw
ms.author: mairaw
ms.date: 09/07/2017
ms.topic: article
ms.prod: .net-core
ms.translationtype: HT
ms.sourcegitcommit: 2943cc58d29323afb81f1c9ae7fc71b538851186
ms.openlocfilehash: e1cb22d78ab9a28cbcd28a99b0b44415b5c46a4d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="net-core-rid-catalog"></a>.NET Core RID 目录

RID 是运行时标识符的缩写。 RID 值用于标识应用程序运行所在的目标平台。
.NET 包使用它们来表示 NuGet 包中特定于平台的资产。 以下值是 RID 的示例：`linux-x64`、`ubuntu.14.04-x64`、`win7-x64` 或 `osx.10.12-x64`。
对于具有本机依赖项的包，RID 将指定在其中可以还原包的平台。

可在项目文件的 `<RuntimeIdentifier>` 元素中设置 RID。 也可使用以下 [.NET Core CLI 命令](./tools/index.md) 通过 `--runtime` 选项使用它们：

- [dotnet build](./tools/dotnet-build.md)
- [dotnet clean](./tools/dotnet-clean.md)
- [dotnet pack](./tools/dotnet-pack.md)
- [dotnet publish](./tools/dotnet-publish.md)
- [dotnet restore](./tools/dotnet-restore.md)
- [dotnet run](./tools/dotnet-run.md)
- [dotnet store](./tools/dotnet-store.md)

表示具体操作系统的 RID 通常遵循以下模式：`[os].[version]-[architecture]-[additional qualifiers]`，其中：

- `[os]` 是操作系统/平台系统名字对象。 例如 `ubuntu`。

- `[version]` 是操作系统版本，使用的格式是以点 (`.`) 分隔的版本号。 例如 `15.10`。

  - 版本不应为营销版本，因为它们通常代表该操作系统的多个离散版本，且具有不同的平台 API 外围应用。

- `[architecture]` 是处理器体系结构。 例如：`x86`、`x64`、`arm` 或 `arm64`。

- `[additional qualifiers]` 进一步区分了不同的平台。 例如 `aot` 或 `corert`。

## <a name="rid-graph"></a>RID 图表

RID 图表或运行时回退图表是互相兼容的 RID 列表。 [Microsoft.NETCore.Platforms](https://www.nuget.org/packages/Microsoft.NETCore.Platforms/) 包中定义了 RID。 可以在 CoreFX 存储库的 [runtime.json](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/runtime.json) 文件中查看支持的 RID 列表和 RID 图表。 在此文件中，可以看到除基 RID 以外的所有 RID 均包含 `"#import"` 语句。 这些语句指示的是兼容的 RID。

NuGet 还原包时，它将尝试找到指定运行时的完全匹配项。
如果未找到完全匹配项，NuGet 将返回此图表，直至它根据 RID 图表找到最相近的兼容系统。

以下示例是 `osx.10.12-x64` RID 的实际条目：

```json
"osx.10.12-x64": {
    "#import": [ "osx.10.12", "osx.10.11-x64" ]
}
```

上述 RID 指定 `osx.10.12-x64` 导入 `osx.10.11-x64`。 因此，当 NuGet 还原包时，它将尝试找到包中的 `osx.10.12-x64` 的完全匹配项。 例如，如果 NuGet 无法找到特定的运行时，可以还原指定 `osx.10.11-x64` 运行时的包。

以下示例演示了 runtime.json 文件中定义的另一个略大的 RID 图表：

```
    win7-x64    win7-x86
       |   \   /    |
       |   win7     |
       |     |      |
    win-x64  |  win-x86
          \  |  /
            win
             |
            any
```

所有 RID 最终都会映射回根 `any` RID。

使用 RID 时，必须牢记以下几个注意事项：

- RID 是不透明字符串，应将其视为黑盒。
- 请勿以编程方式生成 RID。
- 使用已为平台定义的 RID。
- RID 必须具有特定性，因此请勿通过实际的 RID 值假定任何情况。

## <a name="using-rids"></a>使用 RID

若要使用 RID，必须知道有哪些 RID。 新值将定期添加到该平台。
若要获取最新的完整版，请参阅 CoreFX 存储库上的 [runtime.json](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/runtime.json) 文件。

.NET Core 2.0 SDK 引入了可移植 RID 的概念。 它们是添加到 RID 图表的新值，并且未与特定版本或 OS 发行版本关联。 处理多个 Linux 发行版本时，它们非常有用。

以下列表显示了用于每个 OS 的最常见 RID。 其中不包含 `arm` 或 `corert` 值。

## <a name="windows-rids"></a>Windows RID

- 可移植
  - `win-x86`
  - `win-x64`
- Windows 7 / Windows Server 2008 R2
  - `win7-x64`
  - `win7-x86`
- Windows 8 / Windows Server 2012
  - `win8-x64`
  - `win8-x86`
  - `win8-arm`
- Windows 8.1 / Windows Server 2012 R2
  - `win81-x64`
  - `win81-x86`
  - `win81-arm`
- Windows 10 / Windows Server 2016
  - `win10-x64`
  - `win10-x86`
  - `win10-arm`
  - `win10-arm64`

## <a name="linux-rids"></a>Linux RID

- 可移植
  - `linux-x64`
- CentOS
  - `centos-x64`
  - `centos.7-x64`
- Debian
  - `debian-x64`
  - `debian.8-x64`
- Fedora
  - `fedora-x64`
  - `fedora.24-x64`
  - `fedora.25-x64`（.NET Core 2.0 或更高版本）
  - `fedora.26-x64`（.NET Core 2.0 或更高版本）
- Gentoo（.NET Core 2.0 或更高版本）
  - `gentoo-x64`
- openSUSE
  - `opensuse-x64`
  - `opensuse.42.1-x64`
- Oracle Linux
  - `ol-x64`
  - `ol.7-x64`
  - `ol.7.0-x64`
  - `ol.7.1-x64`
  - `ol.7.2-x64`
- Red Hat Enterprise Linux
  - `rhel-x64`
  - `rhel.6-x64`（.NET Core 2.0 或更高版本）
  - `rhel.7-x64`
  - `rhel.7.1-x64`
  - `rhel.7.2-x64`
  - `rhel.7.3-x64`（.NET Core 2.0 或更高版本）
  - `rhel.7.4-x64`（.NET Core 2.0 或更高版本）
- Tizen（.NET Core 2.0 或更高版本）
  - `tizen`
- Ubuntu
  - `ubuntu-x64`
  - `ubuntu.14.04-x64`
  - `ubuntu.14.10-x64`
  - `ubuntu.15.04-x64`
  - `ubuntu.15.10-x64`
  - `ubuntu.16.04-x64`
  - `ubuntu.16.10-x64`
- Ubuntu 衍生内容
  - `linuxmint.17-x64`
  - `linuxmint.17.1-x64`
  - `linuxmint.17.2-x64`
  - `linuxmint.17.3-x64`
  - `linuxmint.18-x64`
  - `linuxmint.18.1-x64`（.NET Core 2.0 或更高版本）

## <a name="os-x-rids"></a>OS X RID

- `osx-x64`（.NET Core 2.0 或更高版本）
- `osx.10.10-x64`
- `osx.10.11-x64`
- `osx.10.12-x64`（.NET Core 1.1 或更高版本）

## <a name="android-rids-net-core-20-or-later-versions"></a>Android RID（.NET Core 2.0 或更高版本）

- `android`
- `android.21`

## <a name="see-also"></a>请参阅
 [运行时 ID](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/readme.md)

