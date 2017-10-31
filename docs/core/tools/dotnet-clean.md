---
title: "dotnet clean 命令 - .NET Core CLI"
description: "dotnet clean 命令可清除当前目录。"
author: mairaw
ms.author: mairaw
ms.date: 08/13/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: 4836f07ec1a8b59c343b4d0181587e602f61d45e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-clean"></a>dotnet-clean

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>名称

`dotnet clean` - 清除项目输出。

## <a name="synopsis"></a>摘要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet clean [<PROJECT>] [-c|--configuration] [-f|--framework] [-o|--output] [-r|--runtime] [-v|--verbosity]
dotnet clean [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet clean [<PROJECT>] [-c|--configuration] [-f|--framework] [-o|--output] [-v|--verbosity]
dotnet clean [-h|--help]
```
---

## <a name="description"></a>描述

`dotnet clean` 命令可清除上一个生成的输出。 它以 [MSBuild 目标](/visualstudio/msbuild/msbuild-targets) 的形式实现，以便在运行命令时对项目进行评估。 只会清除在生成过程中创建的输出。 中间 (*obj*) 和最终输出 (*bin*) 文件夹都会被清除。

## <a name="arguments"></a>参数

`PROJECT`

要清除的 MSBuild 项目。 如果未指定项目文件，MSBuild 会在当前工作目录中搜索以 *proj* 结尾的文件扩展名并使用该文件。

## <a name="options"></a>选项

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`。 只有在生成期间指定了此选项，才必须在清除时使用此选项。

`-f|--framework <FRAMEWORK>`

在生成时指定的[框架](../../standard/frameworks.md)。 必须在[项目文件](csproj.md)中定义该框架。 如果在生成时指定了框架，则必须在清除时指定框架。

`-h|--help`

打印出有关命令的简短帮助。

`-o|--output <OUTPUT_DIRECTORY>`

包含已生成的输出的目录。 如果在生成项目时指定了框架，则使用输出目录开关指定 `-f|--framework <FRAMEWORK>` 开关。

`-r|--runtime <RUNTIME_IDENTIFIER>`

清除指定运行时的输出文件夹。 在创建[独立部署 (SCD)](../deploying/index.md#self-contained-deployments-scd) 时使用此选项。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许的级别为 q[uiet]、m[inimal]、n[ormal]、d[etailed] 和 diag[nostic]。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`。 只有在生成期间指定了此选项，才必须在清除时使用此选项。

`-f|--framework <FRAMEWORK>`

在生成时指定的[框架](../../standard/frameworks.md)。 必须在[项目文件](csproj.md)中定义该框架。 如果在生成时指定了框架，则必须在清除时指定框架。

`-h|--help`

打印出有关命令的简短帮助。

`-o|--output <OUTPUT_DIRECTORY>`

包含已生成的输出的目录。 如果在生成项目时指定了框架，则使用输出目录开关指定 `-f|--framework <FRAMEWORK>` 开关。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许的级别为 q[uiet]、m[inimal]、n[ormal]、d[etailed] 和 diag[nostic]。

---

## <a name="examples"></a>示例

清除项目的默认生成：

`dotnet clean`

清除使用版本配置生成的项目：

`dotnet clean --configuration Release`

