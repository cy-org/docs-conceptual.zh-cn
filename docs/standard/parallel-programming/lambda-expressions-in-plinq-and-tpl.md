---
title: "Lambda Expressions in PLINQ and TPL | Microsoft Docs"
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
  - "Func delegate, creating with lambda expression"
  - "Action delegate, creating with lambda expression"
  - "lambda expressions, with Action and Func"
ms.assetid: 645b2c17-29d0-4ffa-8684-430743cc2f2d
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Lambda Expressions in PLINQ and TPL
任务并行库 \(TPL\) 包含许多方法，这些方法采用委托的 <xref:System.Func%601?displayProperty=fullName> 或 <xref:System.Action?displayProperty=fullName> 系列中的其中一个作为输入参数。  您使用这些委托将自定义程序逻辑传入至并行循环、任务或查询。  TPL 以及 PLINQ 的代码示例使用 lambda 表达式以内联代码块的形式创建这些委托的实例。  本主题简要介绍 Func 和 Action，并演示如何在任务并行库和 PLINQ 中使用 lambda 表达式。  
  
 **注意** 有关委托的更多常规信息，请参见[委托](../Topic/Delegates%20\(C%23%20Programming%20Guide\).md)和 [委托](../Topic/Delegates%20\(Visual%20Basic\).md)。  有关 C\# 和 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中的 lambda 表达式的更多信息，请参见 [Lambda 表达式](../Topic/Lambda%20Expressions%20\(C%23%20Programming%20Guide\).md)和 [lambda 表达式](../Topic/Lambda%20Expressions%20\(Visual%20Basic\).md)。  
  
## Func 委托  
 `Func` 委托封装一个返回值的方法。  在 Func 签名中，最后或最右侧的类型参数始终指定返回类型。  编译器错误的一个常见原因是尝试将两个输入参数传递给一个 <xref:System.Func%602?displayProperty=fullName>；实际上，此类型仅采用一个输入参数。  Framework 类库定义了 17 个版本的 `Func`：<xref:System.Func%601?displayProperty=fullName>、<xref:System.Func%602?displayProperty=fullName>、<xref:System.Func%603?displayProperty=fullName>，诸如此类直至 <xref:System.Func%6017?displayProperty=fullName>。  
  
## Action 委托  
 <xref:System.Action?displayProperty=fullName> 委托封装一个不返回值的方法（[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中为 Sub），或返回 [void](../Topic/void%20\(C%23%20Reference\).md)。  在 Action 类型签名中，类型参数仅表示输入参数。  像 Func 一样，Framework 类库定义了 17 个版本的 Action，从没有类型参数的版本直至具有 16 个类型参数的版本。  
  
## 示例  
 <xref:System.Threading.Tasks.Parallel.ForEach%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%601%7D%2CSystem.Func%7B%60%600%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%601%2C%60%601%7D%2CSystem.Action%7B%60%601%7D%29?displayProperty=fullName> 方法的以下示例演示如何使用 lambda 表达式表达 Func 和 Action 委托。  
  
 [!code-csharp[System.Threading.Tasks.Parallel#02](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.threading.tasks.parallel/cs/parallelforeach.cs#02)]
 [!code-vb[System.Threading.Tasks.Parallel#02](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.threading.tasks.parallel/vb/parallelforeach.vb#02)]  
  
## 请参阅  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)