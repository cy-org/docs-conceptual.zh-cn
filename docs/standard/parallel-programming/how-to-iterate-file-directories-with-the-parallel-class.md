---
title: "如何：使用并行类循环访问文件目录 | Microsoft Docs"
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
  - "并行循环，如何循环访问目录"
ms.assetid: 555e9f48-f53d-4774-9bcf-3e965c732ec5
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用并行类循环访问文件目录
在很多情况下，可以轻松地对文件迭代操作进行并行化。  主题[How to: Iterate File Directories with PLINQ](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-plinq.md)介绍了在很多情况下执行此任务的最简单方式。  然而，如果您的代码必须处理访问文件系统时可能引发的许多类型的异常，情况可能会变得很复杂。  下面的示例演示该问题的一种解决方法。  它使用基于堆栈的迭代遍历指定目录下的所有文件和文件夹，并且它允许您的代码捕获和处理各种异常。  当然，处理异常的方式取决于您。  
  
## 示例  
 下面的示例按顺序循环目录，但是，并行处理文件。  文件与目录的比率较大时，这可能是最佳方法。  还可以并行化目录迭代，并按顺序访问每个文件。  并行化两个循环可能还不够，除非专门针对具有大量处理器的计算机。  然而，与在所有情况下一样，应该全面测试您的应用程序以确定最佳方法。  
  
 [!code-csharp[TPL_Parallel#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_file.cs#08)]
 [!code-vb[TPL_Parallel#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/fileiteration08.vb#08)]  
  
 在此示例中，文件 I\/O 同步执行。  处理大文件或者网络连接较慢时，异步访问文件可能更好。  可以将异步 I\/O 技术与并行循环处理结合使用。  有关详细信息，请参阅[TPL and Traditional .NET Framework Asynchronous Programming](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md)。  
  
 此示例使用本地的 `fileCount` 变量保持全部文件进程的数量。  由于此变量可能被多任务同时访问，所以此访问通过调用 <xref:System.Threading.Interlocked.Add%2A?displayProperty=fullName> 方法进行同步。  
  
 请注意，如果在主线程上引发异常，则 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 方法启动的线程可继续运行。  若要停止这些线程，可以在异常处理程序中设置一个布尔变量，并在并行循环的每次迭代中检查它的值。  如果值表明已引发异常，请使用 <xref:System.Threading.Tasks.ParallelLoopState> 变量停止循环或从循环中断。  有关详细信息，请参阅[How to: Stop or Break from a Parallel.For Loop](http://msdn.microsoft.com/zh-cn/de52e4f1-9346-4ad5-b582-1a4d54dc7f7e)。  
  
## 请参阅  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)