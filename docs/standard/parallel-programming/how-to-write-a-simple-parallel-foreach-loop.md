---
title: "How to: Write a Simple Parallel.ForEach Loop | Microsoft Docs"
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
  - "foreach, parallel version"
  - "parallel programming, foreach"
ms.assetid: cb5fab92-1c19-499e-ae91-8b7525dd875f
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# How to: Write a Simple Parallel.ForEach Loop
本示例显示如何使用 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 循环对任何 <xref:System.Collections.IEnumerable?displayProperty=fullName> 或 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> 数据源启用数据并行。  
  
> [!NOTE]
>  本文档使用 lambda 表达式在 PLINQ 中定义委托。  如果您不熟悉 C\# 或 Visual Basic 中的 lambda 表达式，请参见 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)。  
  
## 示例  
 [!code-csharp[TPL_Parallel#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleforeach.cs#03)]
 [!code-vb[TPL_Parallel#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleforeach.vb#03)]  
  
 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 循环的工作方式类似于 <xref:System.Threading.Tasks.Parallel.For%2A> 循环。  根据系统环境，对源集合进行分区，并在多个线程上计划工作。  系统中的处理器越多，并行方法的运行速度越快。  对于某些源集合，顺序循环可能更快，具体取决于源的大小和正在执行的工作类型。  有关性能的更多信息，请参见[Potential Pitfalls in Data and Task Parallelism](../../../docs/standard/parallel-programming/potential-pitfalls-in-data-and-task-parallelism.md)  
  
 有关并行循环的更多信息，请参见[How to: Write a Simple Parallel.For Loop](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md)  
  
 若要将 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 用于非泛型集合，可以使用 <xref:System.Linq.Enumerable.Cast%2A> 扩展方法将集合转换为泛型集合，如下面的示例所示：  
  
 [!code-csharp[TPL_Parallel#07](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/nongeneric.cs#07)]
 [!code-vb[TPL_Parallel#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/nongeneric.vb#07)]  
  
 还可以使用并行 LINQ \(PLINQ\) 来并行处理 <xref:System.Collections.Generic.IEnumerable%601> 数据源。  PLINQ 使您可以使用声明性的查询语法表达循环行为。  有关更多信息，请参见[Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)。  
  
## 编译代码  
  
-   将此代码复制并粘贴到 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 2010 控制台应用程序项目中。  
  
-   添加对 System.Drawing.dll 的引用  
  
-   按 F5  
  
## 请参阅  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)