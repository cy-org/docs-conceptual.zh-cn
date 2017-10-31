---
title: "dotnet test 命令 - .NET Core CLI"
description: "dotnet test 命令可用于在给定项目中执行单元测试。"
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: 55329bed71be21a787d6e77d8c0ea67d607676b8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-test"></a>dotnet test

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>名称

`dotnet test` - 用于执行单元测试的 .NET 测试驱动程序。

## <a name="synopsis"></a>摘要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)


```
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [--collect] [-d|--diag] [-f|--framework] [--filter] [-l|--logger] [--no-build] [--no-restore] [-o|--output] [-r|--results-directory] [-s|--settings] [-t|--list-tests] [-v|--verbosity]
dotnet test [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [-d|--diag] [-f|--framework] [--filter] [-l|--logger] [--no-build] [-o|--output] [-s|--settings] [-t|--list-tests]  [-v|--verbosity]
dotnet test [-h|--help]
```
---

## <a name="description"></a>描述

`dotnet test` 命令用于执行给定项目中的单元测试。 单元测试是控制台应用程序项目，它包含单元测试框架（如 MSTest、NUnit 或 xUnit）和该框架的 dotnet 测试运行程序上的依赖项。 单元测试打包为 NuGet 包并还原为该项目的普通依赖项。

测试项目还必须指定测试运行程序。 使用普通 `<PackageReference>` 元素指定，如下方示例项目文件所示：

[!code-xml[XUnit 基本模板](../../../samples/snippets/csharp/xunit-test/xunit-test.csproj)]

## <a name="arguments"></a>参数

`PROJECT`

指定测试项目的路径。 如果省略，则默认为当前目录。

## <a name="options"></a>选项

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

在测试运行中使用来自指定路径的自定义测试适配器。

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`，但项目配置可以替代此默认 SDK 设置。

`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`

为测试运行启用数据收集器。 有关详细信息，请参阅[监视和分析测试运行](https://aka.ms/vstest-collect)。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

启用测试平台的诊断模式，并将诊断消息写入指定文件。

`-f|--framework <FRAMEWORK>`

查找特定[框架](../../standard/frameworks.md)的测试二进制文件。

`--filter <EXPRESSION>`

使用给定表达式筛选掉当前项目中的测试。 有关详细信息，请参阅[筛选选项详细信息](#filter-option-details)部分。 有关如何使用选择性单元测试筛选的其他信息和示例，请参阅[运行选择性单元测试](../testing/selective-unit-tests.md)。

`-h|--help`

打印出有关命令的简短帮助。

`-l|--logger <LoggerUri/FriendlyName>`

指定测试结果记录器。

`--no-build`

运行前不生成测试项目。

`--no-restore`

运行此命令时不执行隐式还原。

`-o|--output <OUTPUT_DIRECTORY>`

查找要运行的二进制文件的目录。

`-r|--results-directory <PATH>`

用于放置测试结果的目录。 如果没有，将创建指定目录。

`-s|--settings <SETTINGS_FILE>`

运行测试时要使用的设置。

`-t|--list-tests`

列出当前项目中发现的所有测试。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

在测试运行中使用来自指定路径的自定义测试适配器。

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`，但项目配置可以替代此默认 SDK 设置。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

启用测试平台的诊断模式，并将诊断消息写入指定文件。

`-f|--framework <FRAMEWORK>`

查找特定[框架](../../standard/frameworks.md)的测试二进制文件。

`--filter <EXPRESSION>`

使用给定表达式筛选掉当前项目中的测试。 有关详细信息，请参阅[筛选选项详细信息](#filter-option-details)部分。 有关如何使用选择性单元测试筛选的其他信息和示例，请参阅[运行选择性单元测试](../testing/selective-unit-tests.md)。

`-h|--help`

打印出有关命令的简短帮助。

`-l|--logger <LoggerUri/FriendlyName>`

指定测试结果记录器。

`--no-build`

运行前不生成测试项目。

`-o|--output <OUTPUT_DIRECTORY>`

查找要运行的二进制文件的目录。

`-s|--settings <SETTINGS_FILE>`

运行测试时要使用的设置。

`-t|--list-tests`

列出当前项目中发现的所有测试。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

---

## <a name="examples"></a>示例

运行当前目录所含项目中的测试：

`dotnet test`

运行 `test1` 项目中的测试：

`dotnet test ~/projects/test1/test1.csproj`

## <a name="filter-option-details"></a>筛选选项详细信息

`--filter <EXPRESSION>`

`<Expression>` 格式为 `<property><operator><value>[|&<Expression>]`。

`<property>` 是 `Test Case` 的特性。 下面介绍了常用单元测试框架支持的属性：

| 测试框架 | 支持的属性                                                                                      |
| :------------: | --------------------------------------------------------------------------------------------------------- |
| MSTest         | <ul><li>FullyQualifiedName</li><li>名称</li><li>ClassName</li><li>优先级</li><li>TestCategory</li></ul> |
| Xunit          | <ul><li>FullyQualifiedName</li><li>DisplayName</li><li>特征</li></ul>                                   |

`<operator>` 说明了属性和值之间的关系：

| 运算符 | 函数        |
| :------: | --------------- |
| `=`      | 完全匹配     |
| `!=`     | 非完全匹配 |
| `~`      | 包含        |

`<value>` 是字符串。 所有查找都不区分大小写。

不含 `<operator>` 的表达式自动被视为 `FullyQualifiedName` 属性上的 `contains`（例如，`dotnet test --filter xyz` 与 `dotnet test --filter FullyQualifiedName~xyz` 相同）。

表达式可与条件运算符结合使用：

| 运算符 | 函数 |
| :------: | :------: |
| <code>&#124;</code>      | 或       |
| `&`      | AND      |

使用条件运算符时，可以用括号将表达式括起来（例如，`(Name~TestMethod1) | (Name~TestMethod2)`）。

有关如何使用选择性单元测试筛选的其他信息和示例，请参阅[运行选择性单元测试](../testing/selective-unit-tests.md)。

## <a name="see-also"></a>请参阅

 [框架和目标](../../standard/frameworks.md)   
 [.NET Core 运行时标识符 (RID) 目录](../rid-catalog.md)

