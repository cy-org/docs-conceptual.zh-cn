---
title: "使用 project.json 减少包依赖项"
description: "创建基于 project.json 的库时减少包依赖项。"
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 916251e3-87f9-4eee-81ec-94076215e6fa
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 23d83f0402e35bc4bed31ef59a6fff0e28e01d35
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="reducing-package-dependencies-with-projectjson"></a>使用 project.json 减少包依赖项

本文介绍创作 `project.json` 库时减少包依赖项需要了解的内容。 本文结束后，用户将了解如何撰写库，使其仅使用所需的依赖项。 

## <a name="why-its-important"></a>为什么这十分重要

.NET Core 是由 NuGet 包组成的产品。  基本包为 [.NETStandard.Library 元包](https://www.nuget.org/packages/NETStandard.Library)，它是由其他包组成的 NuGet 包。  它提供保证可在多个 .NET 实现（例如，.NET Framework、.NET Core 和 Xamarin/Mono）上正常工作的包集。

但是，很有可能库将不会使用它所包含的每个包。  当创作库并通过 NuGet 进行分发时，最佳做法是将依赖项“修剪”为仅实际使用的包。  这会使 NuGet 包的总体内存占用变小。

## <a name="how-to-do-it"></a>如何执行此操作

当前，没有任何可修剪包引用的正式 `dotnet` 命令。  相反，需要手动进行此操作。  一般过程如下所示：

1. 在 `project.json` 的 `dependencies` 部分中引用 `NETStandard.Library` 版本 `1.6.0`。
2. 使用 `dotnet restore` 从命令行中还原包。
3. 检查 `project.lock.json` 文件并找到 `NETSTandard.Library` 部分。  它在文件的开头附近。
4. 复制 `dependencies` 下所有列出的包。
5. 删除 `.NETStandard.Library` 引用并将其替换为复制的包。
6. 删除不需要的包引用。

可以通过下面其中一种方式查找不需要的包：

1. 试用和错误。  这包括删除包、还原以及查看库是否仍在编译，并重复此过程。
2. 使用如 [ILSpy](http://ilspy.net) 或 [.NET Reflector](http://www.red-gate.com/products/dotnet-development/reflector) 等工具快速浏览引用，以查看代码实际使用的内容。  然后，可以删除与正在使用的类型不相对应的包。

## <a name="example"></a>示例 

假设编写了一个为泛型集合类型提供其他功能的库。  此类库需要依赖于如 `System.Collections` 的包，但可能根本不会依赖于如 `System.Net.Http` 的包。  因此，将包依赖项修剪为只剩该库所需的依赖项是个好办法！

若要修剪此库，请从 `project.json` 文件开始，然后将引用添加到 `NETStandard.Library` 版本 `1.6.0`。

```json
{
    "version":"1.0.0",
    "dependencies":{
        "NETStandard.Library":"1.6.0"
    },
    "frameworks": {
        "netstandard1.0": {}
     }
}
```

接着，使用 `dotnet restore` 还原包，检查 `project.lock.json` 文件，并查找为 `NETSTandard.Library` 还原的所有包。

以下是以 `netstandard1.0` 为目标时，`project.lock.json` 文件中相关部分的内容：

```json
"NETStandard.Library/1.6.0":{
    "type": "package",
    "dependencies": {
        "Microsoft.NETCore.Platforms": "1.0.1",
        "Microsoft.NETCore.Runtime": "1.0.2",
        "System.Collections": "4.0.11",
        "System.Diagnostics.Debug": "4.0.11",
        "System.Diagnostics.Tools": "4.0.1",
        "System.Globalization": "4.0.11",
        "System.IO": "4.1.0",
        "System.Linq": "4.1.0",
        "System.Net.Primitives": "4.0.11",
        "System.ObjectModel": "4.0.12",
        "System.Reflection": "4.1.0",
        "System.Reflection.Extensions": "4.0.1",
        "System.Reflection.Primitives": "4.0.1",
        "System.Resources.ResourceManager": "4.0.1",
        "System.Runtime": "4.1.0",
        "System.Runtime.Extensions": "4.1.0",
        "System.Text.Encoding": "4.0.11",
        "System.Text.Encoding.Extensions": "4.0.11",
        "System.Text.RegularExpressions": "4.1.0",
        "System.Threading": "4.0.11",
        "System.Threading.Tasks": "4.0.11",
        "System.Xml.ReaderWriter": "4.0.11",
        "System.Xml.XDocument": "4.0.11"
    }
}
```

然后，将包引用复制到库的 `project.json` 文件的 `dependencies` 部分，替换 `NETStandard.Library` 引用：

```json
{
    "version":"1.0.0",
    "dependencies":{
        "Microsoft.NETCore.Platforms": "1.0.1",
        "Microsoft.NETCore.Runtime": "1.0.2",
        "System.Collections": "4.0.11",
        "System.Diagnostics.Debug": "4.0.11",
        "System.Diagnostics.Tools": "4.0.1",
        "System.Globalization": "4.0.11",
        "System.IO": "4.1.0",
        "System.Linq": "4.1.0",
        "System.Net.Primitives": "4.0.11",
        "System.ObjectModel": "4.0.12",
        "System.Reflection": "4.1.0",
        "System.Reflection.Extensions": "4.0.1",
        "System.Reflection.Primitives": "4.0.1",
        "System.Resources.ResourceManager": "4.0.1",
        "System.Runtime": "4.1.0",
        "System.Runtime.Extensions": "4.1.0",
        "System.Text.Encoding": "4.0.11",
        "System.Text.Encoding.Extensions": "4.0.11",
        "System.Text.RegularExpressions": "4.1.0",
        "System.Threading": "4.0.11",
        "System.Threading.Tasks": "4.0.11",
        "System.Xml.ReaderWriter": "4.0.11",
        "System.Xml.XDocument": "4.0.11"
    },
    "frameworks":{
        "netstandard1.0": {}
    }
}
```

这里有相当多的包，其中的许多包对于扩展集合类型来说不是必需的。  可以手动删除包，或者可以使用如 [ILSpy](http://ilspy.net) 或 [.NET Reflector](http://www.red-gate.com/products/dotnet-development/reflector) 等工具来确定代码实际使用的包。

修剪后的包可能如下所示：

```json
{
    "dependencies":{
        "Microsoft.NETCore.Platforms": "1.0.1",
        "Microsoft.NETCore.Runtime": "1.0.2",
        "System.Collections": "4.0.11",
        "System.Linq": "4.1.0",
        "System.Runtime": "4.1.0",
        "System.Runtime.Extensions": "4.1.0",
        "System.Runtime.Handles": "4.0.1",
        "System.Runtime.InteropServices": "4.1.0",
        "System.Runtime.InteropServices.RuntimeInformation": "4.0.0",
        "System.Threading.Tasks": "4.0.11"
    },
    "frameworks":{
        "netstandard1.0": {}
     }
}
```

现在，它比依赖于 `NETStandard.Library` 元包时内存占用更小。

