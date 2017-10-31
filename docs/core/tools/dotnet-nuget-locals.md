---
title: "dotnet nuget locals 命令 - .NET Core CLI"
description: "dotnet nuget locals 命令可清除或列出本地 NuGet 资源，如 http 请求缓存、临时缓存或整个计算机范围内的全局包文件夹。"
author: karann-msft
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: 2b66198ac3e33c640abda0c96fb05944f5ea91df
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-nuget-locals"></a>dotnet nuget locals

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>名称

`dotnet nuget locals` -清除或列出本地 NuGet 资源。

## <a name="synopsis"></a>摘要

`dotnet nuget locals <CACHE_LOCATION> [(-c|--clear)|(-l|--list)] [--force-english-output] [-h|--help]`

## <a name="description"></a>描述

`dotnet nuget locals` 命令清除或列出 http 请求缓存中的本地 NuGet 资源，临时缓存或计算机范围的全局包文件夹。

## <a name="arguments"></a>参数

`CACHE_LOCATION`

以下值之一：

* `all` - 表示指定的操作应用于所有缓存类型，即 http 请求缓存、全局包缓存和临时缓存。
* `http-cache` - 表示指定的操作仅应用于 http 请求缓存。 其他缓存位置不受影响。
* `global-packages` - 表示指定的操作仅应用于全局包缓存。 其他缓存位置不受影响。
* `temp` - 表示指定的操作仅应用于临时缓存。 其他缓存位置不受影响。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

`-c|--clear`

清除选项对指定的缓存类型执行清除操作。 缓存目录的内容被以递归方式删除。 正在执行的用户/组必须具有对缓存目录中的文件的相关权限。 反之，则显示错误，指示未被清除的文件/文件夹。

`-l|--list`

列表选项用于显示指定缓存类型的位置。 

`--force-english-output`

强制命令行输出以英语显示。

## <a name="examples"></a>示例

显示所有本地缓存目录的路径（http 缓存目录、全局包缓存目录和临时缓存目录）：

`dotnet nuget locals –l all`

显示本地 http 缓存录的路径：

`dotnet nuget locals --list http-cache`

清除所有本地缓存目录的文件（http 缓存目录、全局包缓存目录和临时缓存目录）：

`dotnet nuget locals --clear all`

清除本地全局包缓存目录中的所有文件：

`dotnet nuget locals -c global-packages`

清除本地临时缓存目录中的所有文件：

`dotnet nuget locals -c temp`

## <a name="troubleshooting"></a>疑难解答

有关使用 `dotnet nuget locals` 命令时的常见问题和错误的信息，请参阅[管理 NuGet 缓存](/nuget/consume-packages/managing-the-nuget-cache)。
