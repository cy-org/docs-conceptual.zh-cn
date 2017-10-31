---
title: "How to: Handle Exceptions in Parallel Loops | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "parallel loops, how to handle exceptions"
ms.assetid: 512f0d5a-4636-4875-b766-88f20044f143
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# How to: Handle Exceptions in Parallel Loops
<xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 重载没有任何用于处理可能引发的异常的特殊机制。  在这一方面，它们类似于常规 `for` 和 `foreach` 循环（在 Visual Basic 中为 `For` 和 `For Each`）；未处理的异常会导致循环立即终止。  
  
 向并行循环添加自己的异常处理逻辑时，将处理类似于在多个线程上同时引发相似异常的情况，以及一个线程上引发异常导致另一个线程上引发另一个异常的情况。  你可以通过将循环中的所有异常包装到一个 <xref:System.AggregateException?displayProperty=fullName> 中处理这两种情况。  下面的示例演示了一种可能的方法。  
  
> [!NOTE]
>  某些情况下，当启用“仅我的代码”后，Visual Studio 会在引发异常的行中断运行并显示一条错误消息，该消息显示“用户代码未处理异常”。 此错误是良性的。  可以按 F5 继续运行，并请参阅下面示例中所示的异常处理行为。  若要阻止 Visual Studio 在出现第一个错误时中断运行，只需在“工具”、“选项”、“调试”、“常规”下取消选中“仅我的代码”复选框即可。  
  
## 示例  
 在此示例中，所有异常都被捕获，并包装到引发的 <xref:System.AggregateException?displayProperty=fullName> 中。  调用方可以决定要处理哪些异常。  
  
 [!code-csharp[TPL_Exceptions#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptions.cs#08)]
 [!code-vb[TPL_Exceptions#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/exceptionsinloops.vb#08)]  
  
## 请参阅  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)