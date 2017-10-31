---
title: "使用跨平台工具创建 NuGet 包"
description: "了解如何使用“dotnet pack”命令创建 NuGet 包。"
keywords: ".NET、.NET Core、NuGet"
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 2f0415c1-110b-433d-87c1-ae3d543a8844
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9e5c762de0a14407c92c9752edc9619caa07d500
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="how-to-create-a-nuget-package-with-cross-platform-tools"></a>如何使用跨平台工具创建 NuGet 包

> [!NOTE]
> 下例是关于使用 Unix 的命令行。  此处显示的 `dotnet pack` 命令工作方式与在 Windows 上相同。

对于 .NET Core 1.0，所有库都应以 NuGet 包方式发布。  实际上，这是所有 .NET 标准库的发布和使用方式。  可以使用 `dotnet pack` 命令轻松实现此操作。

假设你刚编写了一个很棒的新库，并想通过 NuGet 发布。  你就可以使用跨平台工具创建一个 NuGet 包，完全照做就行！  下例假定使用一个名为 **SuperAwesomeLibrary** 的库，该库以 `netstandard1.0` 为目标。

如果存在可传递的依赖项，也就是说，如果一个项目依赖于另一个项目，在创建 NuGet 包前，则需要确保使用 `dotnet restore` 还原整个解决方案的包。  否则将导致 `dotnet pack` 命令不能正常运行。

确认包已还原后，可以导航到库所在的目录：

`$ cd src/SuperAwesomeLibrary`

然后，只需在命令行中输入一个命令：
    
`$ dotnet pack`

`/bin/Debug` 文件夹现在如下所示：

```
$ ls bin/Debug

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

请注意，这将生成能够进行调试的包。  如果想要生成二进制文件版本的 NuGet 包，只需添加 `-c`/`--configuration` 开关并使用 `release` 作为参数。

`$ dotnet pack --configuration release`

`/bin` 文件夹现在将包含一个 `release` 文件夹，后者包含的 NuGet 包为二进制文件版本：

```
$ ls bin/release

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

因此，现在可以使用此必需的文件发布 NuGet 包了！

## <a name="dont-confuse-dotnet-pack-with-dotnet-publish"></a>不要混淆 `dotnet pack` 和 `dotnet publish`

务必注意，不是任何时候都涉及 `dotnet publish` 命令。  `dotnet publish` 命令用于在同一个包中部署具有所有依赖项的应用程序 - 而不是用于生成通过 NuGet 发布和使用的 NuGet 包。

