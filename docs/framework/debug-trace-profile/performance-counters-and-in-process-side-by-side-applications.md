---
title: "性能计数器和进程内并行应用程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- performance counters
- performance counters,and in-process side-by-side applications
- performance,.NET Framework applications
- performance monitoring,counters
ms.assetid: 6888f9be-c65b-4b03-a07b-df7ebdee2436
caps.latest.revision: 26
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 713aa3a870c42014de01d6782d7452ab60792cc4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="performance-counters-and-in-process-side-by-side-applications"></a>性能计数器和进程内并行应用程序
使用性能监视器 (Perfmon.exe) 有可能在每个运行时基础上区分性能计数器。 本主题介绍启用此功能所需的注册表更改。  
  
## <a name="the-default-behavior"></a>默认行为  
 默认情况下，性能监视器基于每个应用程序显示性能计数器。 但是，这在两种情形下会出现问题：  
  
-   当监视两个名称相同的应用程序时。 例如，如果两个应用程序的名称都为 myapp.exe，二者在“实例”列中将分别显示为“myapp”和“myapp#1”。 在这种情况下很难将性能计数器与特定的应用程序相匹配。 无法确定为“myapp#1”收集的数据指的是第一个 myapp.exe，还是第二个 myapp.exe。  
  
-   当应用程序使用多个公共语言运行时实例时。 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 支持进程内并行承载方案；也就是说，单个进程或应用程序可以加载多个公共语言运行时实例。 如果一个名为 myapp.exe 的应用程序加载两个运行时实例，则默认情况下会在“实例”列中将这两个实例分别指定为“myapp”和“myapp#1”。 在这种情况下，无法确定“myapp”和“myapp#1”指的是两个名称相同的应用程序，还是具有两个运行时的同一应用程序。 如果名称相同的多个应用程序加载多个运行时，则这种歧义性会更大。  
  
 可以设置注册表项来消除此歧义性。 对于使用 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 开发的应用程序，此注册表更改会向“实例”列中的应用程序名称添加一个进程标识符，后跟一个运行时实例标识符。 现在，应用程序将在“实例”列中标识为 application_`p`processID\_`r`runtimeID，而不是 application 或 application#1。 如果应用程序是使用旧版的公共语言运行时开发的，则该实例将表示为 application\_`p`processID，前提是安装了 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]。  
  
## <a name="performance-counters-for-in-process-side-by-side-applications"></a>进程内并行应用程序的性能计数器  
 若要处理单个应用程序中承载的多个公共语言运行时版本的性能计数器，必须如下表所示更改一个注册表项设置。  
  
|||  
|-|-|  
|项名称|HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\\.NETFramework\Performance|  
|值名称|ProcessNameFormat|  
|值类型|REG_DWORD|  
|值|1 (0x00000001)|  
  
 `ProcessNameFormat` 的值为 0 表示启用了默认行为；也就是说，Perfmon.exe 将基于每个应用程序显示性能计数器。 将此值设为 1 时，Perfmon.exe 会明确区分应用程序的多个版本，并基于每个运行时提供性能计数器。 `ProcessNameFormat` 注册表项设置的任何其他值均不受支持，留待将来使用。  
  
 更新 `ProcessNameFormat` 注册表项设置之后，必须重新启动 Perfmon.exe 或任何其他性能计数器的使用方，以便新的实例命名功能可正常工作。  
  
 下面的示例演示如何以编程方式更改 `ProcessNameFormat` 值。  
  
 [!code-csharp[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/cs/regsetting1.cs#1)] [!code-vb[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/vb/regsetting1.vb#1)]  
  
 在进行此注册表更改时，Perfmon.exe 会将面向 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 的应用程序的名称显示为 application_`p`processID\_`r`runtimeID，其中，application 为应用程序的名称，processID 为应用程序的进程标识符，runtimeID 为公共语言运行时标识符。 例如，如果一个名为 myapp.exe 的应用程序加载了两个公共语言运行时实例，Perfmon.exe 可能会将这两个实例分别标识为 myapp_p1416_r10 和 myapp_p3160_r10。 运行时标识符仅可区分进程内的运行时；它不会提供有关运行时的任何其他信息。 （例如，运行时 ID 与运行时的版本或 SKU 无关。）  
  
 如果安装了 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]，注册表更改还会影响使用 .NET Framework 早期版本开发的应用程序。 它们在 Perfmon.exe 中显示为 application_`p`processID，其中，application 为应用程序名称，processID 为进程标识符。 例如，如果监视两个名为 myapp.exe 的应用程序的性能计数器，则这两个应用程序可能分别显示为 myapp_p23900 和 myapp_p24908。  
  
> [!NOTE]
>  进程标识符可消除在解析名称相同且使用运行时早期版本的两个应用程序时存在的歧义性。 因为旧版公共语言运行时不支持并行方案，所以它们不需要运行时标识符。  
  
 如果 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 不存在或已卸载，则设置注册表项不起作用。 这意味着名称相同的两个应用程序在 Perfmon.exe 中将继续显示为 application 和 application#1（例如，myapp 和 myapp#1）。

