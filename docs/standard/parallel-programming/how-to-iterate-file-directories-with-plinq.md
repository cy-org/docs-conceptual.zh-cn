---
title: "How to: Iterate File Directories with PLINQ | Microsoft Docs"
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
  - "PLINQ queries, how to iterate directories"
ms.assetid: 354e8ce3-35c4-431c-99ca-7661d1f3901b
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Iterate File Directories with PLINQ
此示例演示对文件目录执行并行操作的两种简单方式。  第一个查询使用 <xref:System.IO.Directory.GetFiles%2A> 方法填充目录以及所有子目录中文件名的数组。  此方法在填充整个数组之前不返回，因此，可能会在操作开始导致延迟。  但是，填充数组后，PLINQ 可以非常快地并行处理它。  
  
 第二个查询使用静态 <xref:System.IO.Directory.EnumerateDirectories%2A> 和 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> 方法，这两个方法立即开始返回结果。  循环访问大型目录树时，此方法可能更快，但是相对于第一个示例处理时间可能取决于许多因素。  
  
> [!WARNING]
>  这些示例旨在演示用法，运行速度可能不如等效的顺序 LINQ to Objects 查询快。  有关加速的更多信息，请参见[Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
## 示例  
 下面的示例演示如何在下面这种简单的情况中循环访问文件目录：您有权访问树中的所有目录，文件大小不太大，并且访问时间不太多。  此方法在最开始构造文件名数组时有一段时间的延迟。  
  
 [!code-csharp[PLINQ#33](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#33)]  
  
## 示例  
 下面的示例演示如何在下面这种简单的情况中循环访问文件目录：您有权访问树中的所有目录，文件大小不太大，并且访问时间不太多。  此方法比前面的示例更快地开始生成结果。  
  
 [!code-csharp[PLINQ#34](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#34)]  
  
 使用 <xref:System.IO.Directory.GetFiles%2A> 时，请确保您对树中的所有目录具有足够的权限。  否则，将引发一个异常并且不会返回任何结果。  在 PLINQ 查询中使用 <xref:System.IO.Directory.EnumerateDirectories%2A> 时，以允许您继续循环访问的正常方式处理 I\/O 异常存在问题。  如果您的代码必须处理 I\/O 或未授权访问异常，则应考虑[如何：使用并行类循环访问文件目录](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-the-parallel-class.md)中介绍的方法。  
  
 如果 I\/O 延迟成为问题，例如通过网络的文件 I\/O，请考虑使用 [TPL and Traditional .NET Framework Asynchronous Programming](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md)和此[博客文章](http://go.microsoft.com/fwlink/?LinkID=186458)中介绍的某种异步 I\/O 技巧。  
  
## 请参阅  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)