---
title: ".NET Core 支持"
description: "了解 .NET Core 不同版本系列（LTS 和当前版本）支持"
keywords: ".NET, .NET Core, lts, 当前, fts, 支持, 支持系列, 支持跟踪, 生命周期, 版本系列"
author: kendrahavens
ms.author: mairaw
ms.date: 01/30/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: fedc7025-f320-4cba-957b-ef74885f66de
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 254611ef05af22eea616fcfe3288239a744e0ccc
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="net-core-support"></a>.NET Core 支持

本文概述了 .NET Core 支持。

## <a name="lts-and-current-release-trains"></a>LTS 和当前版本系列

提供两个支持版本系列是整个软件领域的一个常见概念，特别是对于开放源代码项目（如 .NET Core）。 .NET Core 提供以下支持版本系列：[长期支持 (LTS)](https://en.wikipedia.org/wiki/Long-term_support) 和当前版本。 维护 LTS 版本是为了在生命周期内确保稳定性，同时接收重要问题的修补程序和安全修补程序。 不同的是，当前版本包含新功能和附加 bug 修补程序。 从支持角度来看，这些版本系列具有以下支持生命周期特性。

LTS 版本
* 自 LTS 版本发布之日起的三年内可获得支持
* 或者，自后续 LTS 版本发布之日起的一年内可获得支持

当前版本
* 与父 LTS 版本一样，在三年内可获得支持
* 自后续当前版本发布之日起的三个月内可获得支持
* 自后续 LTS 版本发布之日起的一年内可获得支持

## <a name="versioning"></a>版本管理
若有新 LTS 版本，主版本号会递增。 当前版本的主版本号与相应的 LTS 系列相同，但次要版本号会递增。 例如，1.0.3 表示 LTS，1.1.0 表示当前版本。 若有 bug 修补程序更新，要么系列会递增，要么修补程序版本号会递增。 有关版本控制方案的详细信息，请参阅 [.NET Core 版本控制](index.md)。

## <a name="what-causes-updates-in-lts-and-current-trains"></a>什么因素会导致 LTS 和当前版本系列发生更新？
若要了解哪些特定更改（如 bug 修补程序或附加 API）会导致版本号发生更新，请查看[版本控制文档](index.md)中的“决策树”部分。 决定要将哪些更改从当前版本拉取到 LTS 版本中时，没有一系列的黄金规则。 通常情况下，必要的安全更新程序和修复预期行为的修补程序会导致 LTS 版本发生更新。 我们还打算在 LTS 版本中支持最新的桌面开发者操作系统，尽管这不是总能实现。 若要及时了解特定版本中支持哪些 API、修补程序和操作系统，一种很好的方式是在 GitHub 上参阅其[版本说明](https://github.com/dotnet/core/tree/master/release-notes)。

### <a name="further-reading"></a>其他阅读材料
* [.NET Core 支持生命周期简报](https://www.microsoft.com/net/core/support)
* [当前支持的操作系统和版本](https://github.com/dotnet/core/blob/master/roadmap.md)

