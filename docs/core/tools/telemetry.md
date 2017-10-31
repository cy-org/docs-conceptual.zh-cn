---
title: ".NET Core CLI 工具遥测"
description: "了解可收集使用情况信息以供分析的 .NET Core 工具遥测功能、收集哪些数据，以及如何禁用遥测。"
keywords: ".NET, .NET Core, 遥测"
author: richlander
ms.author: mairaw
ms.date: 08/04/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 480df976-7568-4df4-9d26-9911357b5a31
ms.translationtype: HT
ms.sourcegitcommit: c58ed1b3c09f1e358d0b66f6cf7186821601fd69
ms.openlocfilehash: 8ea8ee44a58c6aabfd09afbc7ef53239a9029c57
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---

# <a name="net-core-cli-tools-telemetry"></a>.NET Core CLI 工具遥测

[.NET Core SDK](index.md) 包括可收集使用情况信息的[遥测功能](https://github.com/dotnet/cli/pull/2145)。 请务必让 .NET 团队了解到工具使用情况，以便我们可以进行改进。 有关详细信息，请参阅[从 .NET Core SDK 遥测中所了解到的内容](https://blogs.msdn.microsoft.com/dotnet/2017/07/21/what-weve-learned-from-net-core-sdk-telemetry/)。

数据为匿名收集，并以汇总形式发布，以供 Microsoft 和社区根据 [Creative Commons Attribution 许可证](https://creativecommons.org/licenses/by/4.0/)使用。 

## <a name="scope"></a>范围

`dotnet` 命令用于启动应用程序和 .NET Core CLI。 `dotnet` 命令本身不收集遥测数据。 `dotnet` 命令运行的 .NET Core CLI 命令收集遥测数据。

使用 `dotnet` 命令本身且没有附加任何命令时，不会启用遥测：

- `dotnet`
- `dotnet [path-to-app]`

使用 [.NET Core CLI 命令](index.md)时，就会启用遥测，如：

- `dotnet build`
- `dotnet pack`
- `dotnet restore`
- `dotnet run`

## <a name="behavior"></a>行为

.NET Core CLI 工具遥测功能默认处于启用状态。 通过将 `DOTNET_CLI_TELEMETRY_OPTOUT` 环境变量设置为 `1` 或 `true`，可以选择退出遥测功能。

## <a name="data-points"></a>数据点

此功能收集以下数据：

- 调用时间戳&#8224;
- 调用的命令（例如，“build”）&#8224;
- 用于确定地理位置的三个八进制数 IP 地址&#8224;
- 命令的 `ExitCode`
- 测试运行程序（对于测试项目）
- 操作系统和版本&#8224;
- “运行时”节点中是否有运行时 ID
- .NET Core SDK 版本&#8224;

&#8224;此指标已发布。

自 .NET Core SDK 2.0 起，收集以下新数据点：

- `dotnet` 命令参数和选项：仅收集已知参数和选项（非任意字符串）。
- SDK 是否在容器中运行。
- 目标框架。
- 经过哈希处理的 MAC 地址：计算机的加密 (SHA256) 匿名的唯一 ID。 此指标未发布。
- 经过哈希处理的当前工作目录。

此功能不收集用户名或电子邮件地址等个人数据。 也不会扫描代码，亦不会提取项目级敏感数据，如名称、存储库或作者。 数据通过 [Microsoft Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 技术安全地发送到 Microsoft 服务器，提供对保留数据的受限访问权限，并在严格的安全控制下从安全 [Azure 存储](https://azure.microsoft.com/services/storage/)系统发布。

我们需要知道工具使用情况及其是否在正常运行，而不是使用这些工具生成的内容。 如果怀疑遥测在收集敏感数据，或认为我们处理数据的方式不安全或不恰当，请[在 dotnet/cli 存储库问题中记录问题](https://github.com/dotnet/cli/issues)以供调查。

## <a name="published-data"></a>已发布的数据

数据每季度发布一次，并在 [.NET Core SDK 使用情况数据](https://github.com/dotnet/core/blob/master/release-notes/cli-usage-data.md)中列出。 数据文件列如下：
- 时间戳
- Occurrences&#8224;
- 命令
- Geography&#8225;
- OSFamily
- RuntimeID
- OSVersion
- SDKVersion

&#8224;Occurrences 列显示相应命令当天用于该行指标的总次数。 

&#8225;通常情况下，Geography 列显示国家/地区名称。 在某些情况下，此列中会显示南极洲，要么是因为研究人员在南极洲使用 .NET Core，要么是因为位置数据不正确。

### <a name="example"></a>示例

| 时间戳      | Occurrences | 命令 | Geography | OSFamily | RuntimeID     | OSVersion | SDKVersion |
| -------------- | ----------- | ------- | --------- | -------- | ------------- | --------- | ---------- |
| 4/16/2017 0:00 | 8           | 运行     | Uganda    | Darwin   | osx.10.12-x64 | 10.12     | 1.0.1      |

### <a name="datasets"></a>数据集

[2016 - Q3](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2016-q3.tsv)  
[2016 - Q4](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2016-q4.tsv)  
[2017 - Q1](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2017-q1.tsv)  
[2017 - Q2](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2017-q2.tsv)

其他数据集使用标准的 URL 格式进行发布。 请将 `<YEAR>` 替换为相应年份，并将 `<QUARTER>` 替换为相应季度（使用 `1`、`2`、`3` 或 `4`）。 文件采用制表符分隔值 (TSV) 格式。 

```
https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-<YEAR>-q<QUARTER>.tsv
```

## <a name="license"></a>许可证

.NET Core 的 Microsoft 分发由 [MICROSOFT .NET LIBRARY EULA](https://aka.ms/dotnet-core-eula) 授权。 此许可证包括“DATA”部分，用于启用遥测（如下所示）。

[.NET NuGet 包](https://www.nuget.org/profiles/dotnetframework)使用相同许可证，但不启用遥测（见[范围](#scope)）。

> 2. DATA。 此软件可能会收集并向 Microsoft 发送你的信息和软件使用信息。 Microsoft 可能会使用此类信息来改进我们的产品和服务。 可以参阅帮助文档和隐私声明 (http://go.microsoft.com/fwlink/?LinkId=528096)，详细了解数据收集和使用。 使用此软件即表示同意接受这些做法。

## <a name="disclosure"></a>公开

.NET Core CLI 工具在用户首次运行其中一个命令（例如，`dotnet restore`）时显示以下文本。 文本可能会因运行的 SDK 版本而略有不同。 此“首次运行”体验是 Microsoft 通知用户有关数据收集信息的方式。

```console
Welcome to .NET Core!
---------------------
Learn more about .NET Core @ https://aka.ms/dotnet-docs. Use dotnet --help to see available commands or go to https://aka.ms/dotnet-cli-docs.
 
Telemetry
--------------
The .NET Core tools collect usage data in order to improve your experience. The data is anonymous and does not include command-line arguments. The data is collected by Microsoft and shared with the community.
You can opt out of telemetry by setting a DOTNET_CLI_TELEMETRY_OPTOUT environment variable to 1 using your favorite shell.
You can read more about .NET Core tools telemetry @ https://aka.ms/dotnet-cli-telemetry.
```

## <a name="see-also"></a>另请参阅

[从 .NET Core SDK 遥测中所了解到的内容](https://blogs.msdn.microsoft.com/dotnet/2017/07/21/what-weve-learned-from-net-core-sdk-telemetry/)  
[遥测参考源（dotnet/cli 存储库；版本/2.0.0 分支）](https://github.com/dotnet/cli/blob/release/2.0.0/src/dotnet/Telemetry.cs)   
[.NET Core SDK 使用情况数据](https://github.com/dotnet/core/blob/master/release-notes/cli-usage-data.md)

