---
title: "dotnet sln 命令 - .NET Core CLI"
description: "使用 dotnet-sln 命令，可以便捷地在解决方案文件中添加、删除和列出项目。"
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: 5071cb80be0fb14829a0fdffd0f5a2d2371b6ba8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-sln"></a>dotnet sln

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>名称

`dotnet-sln` - 修改 .NET Core 解决方案文件。

## <a name="synopsis"></a>摘要

```
dotnet sln [<SOLUTION_NAME>] add <PROJECT> <PROJECT> ...
dotnet sln [<SOLUTION_NAME>] add <GLOBBING_PATTERN>
dotnet sln [<SOLUTION_NAME>] remove <PROJECT> <PROJECT> ...
dotnet sln [<SOLUTION_NAME>] remove <GLOBBING_PATTERN>
dotnet sln [<SOLUTION_NAME>] list
dotnet sln [-h|--help]
```

## <a name="description"></a>描述

使用 `dotnet sln` 命令，可以便捷地在解决方案文件中添加、删除和列出项目。

## <a name="commands"></a>命令

`add <PROJECT> ...`

`add <GLOBBING_PATTERN>`

将一个或多个项目添加到解决方案文件中。 基于 Unix/Linux 的终端支持[通配模式](https://en.wikipedia.org/wiki/Glob_(programming))。

`remove <PROJECT> ...`

`remove <GLOBBING_PATTERN>`

从解决方案文件中删除一个或多个项目。 基于 Unix/Linux 的终端支持[通配模式](https://en.wikipedia.org/wiki/Glob_(programming))。

`list`

列出解决方案文件中的所有项目。

## <a name="arguments"></a>参数

`SOLUTION_NAME`

要使用的解决方案文件。 如果未指定，此命令会搜索当前目录来获取一个项目文件。 如果目录中有多个解决方案文件，必须指定一个。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

## <a name="examples"></a>示例

将一个 C# 项目添加到解决方案中：

`dotnet sln todo.sln add todo-app/todo-app.csproj`

从解决方案中删除一个 C# 项目：

`dotnet sln todo.sln remove todo-app/todo-app.csproj`

将多个 C# 项目添加到解决方案中：

`dotnet sln todo.sln add todo-app/todo-app.csproj back-end/back-end.csproj`

从解决方案中删除多个 C# 项目：

`dotnet sln todo.sln remove todo-app/todo-app.csproj back-end/back-end.csproj`

使用通配模式将多个 C# 项目添加到解决方案中：

`dotnet sln todo.sln add **/*.csproj`

使用通配模式从解决方案中删除多个 C# 项目：

`dotnet sln todo.sln remove **/*.csproj`
