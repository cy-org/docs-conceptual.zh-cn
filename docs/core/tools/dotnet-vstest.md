---
title: "dotnet vstest 命令 - .NET Core CLI"
description: "dotnet vstest 命令可生成项目及其所有依赖项。"
author: guardrex
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: c5a7ee0ba306cea641b0ff34f0b521c92bd03719
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-vstest"></a>dotnet vstest

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>名称

`dotnet-vstest` - 从指定文件运行测试。

## <a name="synopsis"></a>摘要

`dotnet vstest [<TEST_FILE_NAMES>] [--Settings|/Settings] [--Tests|/Tests] [--TestAdapterPath|/TestAdapterPath] [--Platform|/Platform] [--Framework|/Framework] [--Parallel|/Parallel] [--TestCaseFilter|/TestCaseFilter] [--logger|/logger] [-lt|--ListTests|/lt|/ListTests] [--ParentProcessId|/ParentProcessId] [--Port|/Port] [--Diag|/Diag] [[--] <args>...]] [-?|--Help|/?|/Help]`

## <a name="description"></a>说明

`dotnet-vstest` 命令运行 `VSTest.Console` 命令行应用程序以运行自动化单元测试和编码的 UI 应用程序测试。

## <a name="arguments"></a>参数

`TEST_FILE_NAMES`

从指定的程序集运行测试。 用空格分隔多个测试程序集名称。

## <a name="options"></a>选项

`--Settings|/Settings:<Settings File>`

运行测试时要使用的设置。

`--Tests|/Tests:<Test Names>`

运行具有与提供的值匹配的名称的测试。 用逗号分隔多个值。

`--TestAdapterPath|/TestAdapterPath`

在测试运行中使用来自给定路径（如果有）的自定义测试适配器。

`--Platform|/Platform:<Platform type>`

用于执行测试的目标平台体系结构。 有效值为 `x86`、`x64` 和 `ARM`。

`--Framework|/Framework:<Framework Version>`

用于测试执行的目标 .NET Framework 版本。 有效值的示例为 `.NETFramework,Version=v4.6`、`.NETCoreApp,Version=v1.0` 等。其他支持的值为 `Framework35`、`Framework40`、`Framework45` 和 `FrameworkCore10`。

`--Parallel|/Parallel`

并行执行测试。 默认情况下，计算机上的所有可用内核都可供使用。 使用设置文件设置显式内核数量。

`--TestCaseFilter|/TestCaseFilter:<Expression>`

运行与给定表达式匹配的测试。 `<Expression>` 的格式为 `<property>Operator<value>[|&<Expression>]`，其中运算符是 `=`、`!=` 或 `~` 之一。  运算符 `~` 具有“包含”语义，并适用于字符串属性，如 `DisplayName`。 括号 `()` 用于组的子表达式。

`-?|--Help|/?|/Help`

打印出有关命令的简短帮助。

`--logger|/logger:<Logger Uri/FriendlyName>`

为测试结果指定一个记录器。  

* 若要将测试结果发布到 Team Foundation Server，请使用 `TfsPublisher` 记录器提供程序：

  ```
  /logger:TfsPublisher;
      Collection=<team project collection url>;
      BuildName=<build name>;
      TeamProject=<team project name>
      [;Platform=<Defaults to "Any CPU">]
      [;Flavor=<Defaults to "Debug">]
      [;RunTitle=<title>]
  ```

* 若要将结果记录到 Visual Studio 测试结果文件 (TRX)，请使用 `trx` 记录器提供程序。 此开关使用给定的日志文件名在测试结果目录中创建一个文件。 如果未提供 `LogFileName`，将创建唯一的文件名以保留测试结果。

  ```
  /logger:trx [;LogFileName=<Defaults to unique file name>]
  ```

`-lt|--ListTests|/lt|/ListTests:<File Name>`

列出给定测试容器中的已发现的测试。

`--ParentProcessId|/ParentProcessId:<ParentProcessId>`

父进程的进程 ID 负责启动当前进程。

`--Port|/Port:<Port>`

指定套接字连接和接收事件消息的端口。

`--Diag|/Diag:<Path to log file>`

为测试平台启用详细日志。 日志被写入到所提供的文件。

`args`

指定要传递到适配器的额外参数。 参数被指定为 `<n>=<v>` 格式的名称值对，其中 `<n>` 是参数名称，`<v>` 是参数值。 使用空格分隔多个参数。

## <a name="examples"></a>示例

在 `mytestproject.dll` 中运行测试：

`dotnet vstest mytestproject.dll`

在 `mytestproject.dll` 和 `myothertestproject.exe` 中运行测试：

`dotnet vstest mytestproject.dll myothertestproject.exe`

运行 `TestMethod1` 测试：

`dotnet vstest /Tests:TestMethod1`

运行 `TestMethod1` 和 `TestMethod2` 测试：

`dotnet vstest /Tests:TestMethod1,TestMethod2`

