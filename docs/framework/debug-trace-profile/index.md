---
title: "调试、跟踪和分析"
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
- debugging [.NET Framework]
- .NET Framework application configuration, debugging
- debugging [.NET Framework], .NET Framework application debugging
- troubleshooting applications [.NET Framework], profiling
- application development [.NET Framework], debugging
- .NET Framework application configuration, profiling
- profiling applications
- troubleshooting applications [.NET Framework], debugging
- troubleshooting applications [.NET Framework]
- application development [.NET Framework], profiling
ms.assetid: 4a04863e-2475-46f4-bc3f-3c11510c2a4b
caps.latest.revision: 28
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1f7696edacc95dee383a7c7e9256cca3eac44839
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="debugging-tracing-and-profiling"></a>调试、跟踪和分析
若要调试 .NET Framework 应用程序，编译器和运行时环境必须配置为可将调试程序附加到该应用程序，并且如果可能的话，为该应用程序及其相应 Microsoft 中间语言 (MSIL) 同时生成符号和行映射。 在对托管应用程序进行调试后，可对其进行分析以增强性能。 分析计算并描述可生成最常执行的代码的源代码行，以及执行它们所需的时间。  
  
 通过使用 Visual Studio 可轻松地调试.NET framework 应用程序，前者用于处理配置的许多详细信息。 如果未安装 Visual Studio，可以通过使用 .NET Framework <xref:System.Diagnostics> 命名空间中的调试类检查并提升 .NET Framework 应用程序的性能。 此命名空间包括用于跟踪执行流的 <xref:System.Diagnostics.Trace>、<xref:System.Diagnostics.Debug> 和 <xref:System.Diagnostics.TraceSource> 类，以及用于分析代码的 <xref:System.Diagnostics.Process>、<xref:System.Diagnostics.EventLog> 和 <xref:System.Diagnostics.PerformanceCounter> 类。  
  
## <a name="in-this-section"></a>本节内容  
 [启用 JIT 附加调试](../../../docs/framework/debug-trace-profile/enabling-jit-attach-debugging.md)  
 演示如何配置注册表从而将调试引擎以 JIT 方式附加到 .NET Framework 应用程序。  
  
 [使映像更易于调试](../../../docs/framework/debug-trace-profile/making-an-image-easier-to-debug.md)  
 演示如何打开 JIT 跟踪和关闭优化，以使程序集更易于调试。  
  
 [跟踪应用程序和在应用程序中插入检测点](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)  
 描述如何监视应用程序在运行时的执行，以及如何来检测它以显示其执行状态或是否出现了问题。  
  
 [使用托管调试助手诊断错误](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)  
 描述托管调试助手 (MDA)，它是与公共语言运行时 (CLR) 联合工作以提供有关运行时状态信息的调试辅助程序。  
  
 [使用调试器显示特性增强调试](../../../docs/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes.md)  
 描述某种类型的开发人员可如何指定该类型在调试器中显示时的样子。  
  
 [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md)  
 描述可用来跟踪应用程序性能的计数器。  
  
## <a name="related-sections"></a>相关章节  
 [调试 ASP.NET 和 AJAX 应用程序](http://msdn.microsoft.com/library/9d531913-541b-47b8-864d-138021fca0c6)  
 提供有关如何在开发期间或部署后调试 ASP.NET 应用程序的先决条件和说明。  
  
 [开发指南](../../../docs/framework/development-guide.md)  
 提供了有关应用程序开发的所有关键技术区域和任务（包括创建、配置、调试、保护和部署应用程序）的指南，以及有关动态编程、互操作性、扩展性、内存管理和线程处理的信息。

