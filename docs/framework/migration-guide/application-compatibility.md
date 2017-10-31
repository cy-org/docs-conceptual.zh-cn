---
title: ".NET Framework 中的应用程序兼容性"
ms.custom: 
ms.date: 05/19/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
- app-compat
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application compatibility
- .NET Framework application compatibility
- .NET Framework changes
caps.latest.revision: 19
ms.assetid: c4ba3ff2-fe59-4c5d-9e0b-86bba3cd865c
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: b3c7df2984c2c9e8af308ca8070f7207d11ba49e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="application-compatibility-in-the-net-framework"></a>.NET Framework 中的应用程序兼容性

## <a name="introduction"></a>介绍

兼容性是每版 .NET 要实现的非常重要的目标。 兼容性可确保每个版本都具有累加特征，以便旧版本仍能正常使用。 然而，更改旧功能（以便提升性能、解决安全问题或修复 bug）可能会导致在更高版本 .NET 上运行的现有代码或应用出现兼容性问题。 .NET Framework 可识别重定目标更改和运行时更改。 重定目标更改会影响定位特定版本的 .NET Framework、但在更高版本 .NET 上运行的应用。 运行时更改会影响在特定版本 .NET 上运行的所有应用。

每个应用都定位特定版本的 .NET Framework，这可以通过下列方式指定：

- 在 Visual Studio 中定义目标框架。
- 在项目文件中指定目标框架。
- 向源代码应用 <xref:System.Runtime.Versioning.TargetFrameworkAttribute>。

如果应用在比目标 .NET 版本更高的版本上运行，.NET Framework 会通过怪异的行为来模拟旧版目标版本。 也就是说，应用虽然在更高版本的 Framework 上运行，但行为就像在旧版本 .NET 上运行一样。 .NET Framework 各版本之间的许多兼容性问题都是通过这种怪异的模型进行缓解。

## <a name="runtime-changes"></a>运行时更改

运行时问题是指当新的运行时出现在计算机上、运行的二进制文件相同、但行为不同时出现的问题。 如果二进制文件的编译目标为 .NET Framework 4.0，它将在 4.5 或更高版本上的 .NET Framework 4.0 兼容性模式下运行。 许多影响 4.5 的更改将不会影响编译目标为 4.0 的二进制文件。 这是 AppDomain 才会出现的问题，具体视输入程序集的设置而定。

## <a name="retargeting-changes"></a>重定目标更改

重定目标问题是指当原本定位 4.0 的程序集现在设为定位 4.5 时出现的问题。 此时，程序集启用新功能，并存在与旧功能的潜在兼容性问题。 再强调一遍，这取决于输入程序集，同样也取决于使用此程序集的控制台应用或引用此程序集的网站。

## <a name="net-compatibility-diagnostics"></a>.NET 兼容性诊断

.NET 兼容性诊断是 Roslyn 提供技术支持的分析器，有助于确定 .NET Framework 不同版本之间的应用程序兼容性问题。 此列表包含所有可用的分析器，尽管仅部分分析器适用于任何具体的迁移。 这些分析器可确定计划迁移会发生的问题，并仅显示这些问题。

每个问题包含以下信息：

-   从以前版本发生的更改的介绍。

-   更改对客户造成了哪些影响，以及是否有任何解决办法可以保持各版本的兼容性。

-   对于更改重要性的评估。 应用程序兼容性问题可分成以下几类：

    |   |   |
    |---|---|
    |主要|影响大量应用或需要修改大量代码的重大更改。|
    |次要|影响少量应用或需要修改少量代码的更改。|
    |边缘情况|在极少数特定的情况下影响应用的更改。|
    |透明|对应用开发者或用户没有造成显著影响的更改。|

-   版本指示了更改首次出现在框架中的时间。 某些更改会在特定版本中引入，并在以后的版本中进行还原；这也会在版本中指出。

-   更改类型：

    |   |   |
    |---|---|
    |重定目标|更改会影响重新编译以面向新版 .NET Framework 的应用。|
    |运行时|更改会影响面向以前版本的 .NET Framework 但在更高版本上运行的现有应用。|

-   受影响的 API（如果有）。

-   可用诊断的 ID

## <a name="usage"></a>用法

首先，从下面选择一种兼容性更改类型：

- [重定目标更改](./retargeting/index.md)
- [运行时更改](./runtime/index.md)


## <a name="see-also"></a>请参阅

[版本和依赖关系](../../../docs/framework/migration-guide/versions-and-dependencies.md)   
[新增功能](../../../docs/framework/whats-new/index.md)   
[类库中过时的内容](../../../docs/framework/whats-new/whats-obsolete.md)

