---
title: "How to: Unwrap a Nested Task | Microsoft Docs"
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
  - "tasks, how to unwrap nested tasks"
ms.assetid: a0769dd2-0f6d-48ca-8418-a9d39de7f450
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Unwrap a Nested Task
您可以从方法中返回任务，然后等待或从该任务中继续，如下面的示例所示：  
  
 [!code-csharp[TPL_Unwrap#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#01)]
 [!code-vb[TPL_Unwrap#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippets1-3.vb#01)]  
  
 在前面的示例中，<xref:System.Threading.Tasks.Task%601.Result%2A> 属性的类型为 `string`（在 Visual Basic 中为 `String`）。  
  
 但是，在某些情况下，您可能需要在另一个任务内创建任务，然后返回嵌套任务。  在这种情况下，封闭任务的 `TResult` 本身也是任务。  在下面的示例中，Result 属性为 `Task<Task<string>>`（在 C\# 中）或 `Task(Of Task(Of String))`（在 Visual Basic 中）。  
  
 [!code-csharp[TPL_Unwrap#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#02)]
 [!code-vb[TPL_Unwrap#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippets1-3.vb#02)]  
  
 尽管可以编写代码来解除外部任务的包装并检索原始任务及其 <xref:System.Threading.Tasks.Task%601.Result%2A> 属性，但此代码并不容易编写，因为您必须处理异常和取消请求。  在这种情况下，我们建议您使用 <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> 扩展方法之一，如下面的示例所示。  
  
 [!code-csharp[TPL_UnWrap#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#03)]
 [!code-vb[TPL_UnWrap#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippets1-3.vb#03)]  
  
 可以使用 <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> 方法将任何 `Task<Task>` 或 `Task<Task<TResult>>`（在 Visual Basic 中为 `Task(Of Task)` 或 `Task(Of Task(Of TResult))`）转换为 `Task` 或 `Task<TResult>` （在 Visual Basic 中为 `Task(Of TResult)`）。  新任务将完整表示内部嵌套任务，并包括取消状态和所有异常。  
  
## 示例  
 下面的示例演示如何使用 <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> 扩展方法。  
  
 [!code-csharp[TPL_UnWrap#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#04)]
 [!code-vb[TPL_UnWrap#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippet04.vb#04)]  
  
## 请参阅  
 <xref:System.Threading.Tasks.TaskExtensions?displayProperty=fullName>   
 [Task Parallelism](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)