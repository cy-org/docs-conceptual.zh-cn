---
title: "公共语言运行时中的程序集"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dynamic assemblies
- security [.NET Framework], boundaries
- boundaries of assemblies
- assemblies [.NET Framework], about
- assemblies [.NET Framework], boundaries
- reference scope boundaries
- assemblies [.NET Framework]
- version boundaries
- type boundaries
ms.assetid: 2cfebe19-7436-49f1-bd99-3c4019f0b676
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: faa41efa7f3ad898557e966d141aa8f5108d60bd
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="assemblies-in-the-common-language-runtime"></a>公共语言运行时中的程序集
程序集是 .NET Framework 应用程序的构造块；它们形成了部署、版本控制、重复使用、激活范围和安全权限的基本单元。 程序集是为协同工作而生成的类型和资源的集合，这些类型和资源构成了一个逻辑功能单元。 程序集向公共语言运行时提供了解类型实现所需要的信息。 对于运行时，类型不存在于程序集上下文之外。  
  
 程序集执行以下功能：  
  
-   包含公共语言运行时执行的代码。 如果可迁移可执行 (PE) 文件没有相关联的程序集清单，则将不执行该文件中的 Microsoft 中间语言 (MSIL) 代码。 请注意，每个程序集只能有一个入口点（即 `DllMain`、`WinMain` 或 `Main`）。  
  
-   程序集形成安全边界。 程序集就是在其中请求和授予权限的单元。 有关应用于程序集的安全边界的更多信息，请参见[程序集安全注意事项](../../../docs/framework/app-domains/assembly-security-considerations.md)。  
  
-   程序集形成类型边界。 每一类型的标识均包括该类型所驻留的程序集的名称。 在一个程序集的范围中加载的称为 `MyType` 的类型不同于在另一个程序集范围中加载的称为 `MyType` 的类型。  
  
-   程序集形成引用范围边界。 程序集的清单包含用于解析类型和满足资源请求的程序集元数据。 它指定在该程序集之外公开的类型和资源。 该清单还枚举它所依赖的其他程序集。  
  
-   程序集形成版本边界。 程序集是公共语言运行时中最小的可版本化单元，同一程序集中的所有类型和资源均会被版本化为一个单元。 程序集的清单描述你为任何依赖项程序集所指定的版本依赖性。 有关版本控制的更多信息，请参见[程序集版本控制](../../../docs/framework/app-domains/assembly-versioning.md)。  
  
-   程序集形成部署单元。 当一个应用程序启动时，只有该应用程序最初调用的程序集必须存在。 其他程序集（例如本地化资源和包含实用工具类的程序集）可以按需检索。 这就使应用程序在第一次下载时保持精简。 有关部署程序集的更多信息，请参见[部署应用程序](../../../docs/framework/deployment/index.md)。  
  
-   程序集是支持并行执行的单元。 有关运行多个程序集版本的更多信息，请参见[程序集和并行执行](../../../docs/framework/app-domains/assemblies-and-side-by-side-execution.md)。  
  
 程序集可以为静态或动态。 静态程序集可以包括 .NET Framework 类型（接口和类），以及该程序集的资源（位图、JPEG 文件、资源文件等）。 静态程序集存储在磁盘上的可迁移可执行 (PE) 文件中。 你还可以使用 .NET Framework 来创建动态程序集，动态程序集直接从内存运行并且在执行前不存储到磁盘上。 你可以在执行动态程序集后将它们保存在磁盘上。  
  
 有几种创建程序集的方法。 你可以使用过去用来创建 .dll 或 .exe 文件的开发工具，例如 Visual Studio。 你可以使用 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] 中提供的工具创建带有在其他部署环境中创建的模块的程序集。 还可以使用公共语言运行时 API（例如 <xref:System.Reflection.Emit?displayProperty=fullName>）来创建动态程序集。  
  
## <a name="related-topics"></a>相关主题  
  
|标题|说明|  
|-----------|-----------------|  
|[程序集内容](../../../docs/framework/app-domains/assembly-contents.md)|描述组成程序集的各元素。|  
|[程序集清单](../../../docs/framework/app-domains/assembly-manifest.md)|描述程序集清单中的数据，以及它如何存储在程序集中。|  
|[全局程序集缓存](../../../docs/framework/app-domains/gac.md)|描述全局程序集缓存以及它如何用于程序集。|  
|[具有强名称的程序集](../../../docs/framework/app-domains/strong-named-assemblies.md)|描述具有强名称的程序集的特性。|  
|[程序集安全注意事项](../../../docs/framework/app-domains/assembly-security-considerations.md)|讨论安全性如何作用于程序集。|  
|[程序集版本控制](../../../docs/framework/app-domains/assembly-versioning.md)|提供对 .NET Framework 版本控制策略的概述。|  
|[程序集位置](../../../docs/framework/app-domains/assembly-placement.md)|讨论将程序集放到什么位置。|  
|[程序集和并行执行](../../../docs/framework/app-domains/assemblies-and-side-by-side-execution.md)|提供同时使用运行时或程序集的多个版本的概述。|  
|[使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)|描述如何在程序集上创建、签署和设置特性。|  
|[发出动态方法和程序集](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)|描述如何创建动态程序集。|  
|[运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)|描述 .NET Framework 如何在运行时解析程序集引用。|  
  
## <a name="reference"></a>参考  
 <xref:System.Reflection.Assembly?displayProperty=fullName>

