---
title: "如何：枚举打印队列的子集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "枚举, 打印队列的子集"
  - "打印队列, 枚举子集"
ms.assetid: cc4a1b5b-d46f-4c5e-bc26-22c226e4bee0
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：枚举打印队列的子集
负责管理公司范围内打印机的信息技术 \(IT\) 专家所面临的一个共同任务是，生成具有某些特征的打印机的列表。  该功能由 <xref:System.Printing.PrintServer> 对象的 <xref:System.Printing.PrintServer.GetPrintQueues%2A> 方法以及 <xref:System.Printing.EnumeratedPrintQueueTypes> 枚举来提供。  
  
## 示例  
 在下面的示例中，代码首先创建一个标志数组来指定要列出的打印队列的特征。  在本示例中，我们要查找安装在打印服务器本地且处于共享状态的打印队列。  <xref:System.Printing.EnumeratedPrintQueueTypes> 枚举提供许多其他功能。  
  
 该代码随后创建一个 <xref:System.Printing.LocalPrintServer> 对象，这是一个派生自 <xref:System.Printing.PrintServer> 的类。  本地打印服务器是运行应用程序的计算机。  
  
 最后一个重要的步骤是将该数组传递给 <xref:System.Printing.PrintServer.GetPrintQueues%2A> 方法。  
  
 最后，结果将呈现给用户。  
  
 [!code-cpp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](../../../../samples/snippets/cpp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CPP/Program.cpp#listsubsetofprintqueues)]
 [!code-csharp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CSharp/Program.cs#listsubsetofprintqueues)]
 [!code-vb[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/visualbasic/program.vb#listsubsetofprintqueues)]  
  
 可以通过让单步执行每个打印队列的 `foreach` 循环执行进一步筛选来扩展此示例。  例如，可以通过让该循环调用每个打印队列的 <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A> 方法并对双面打印存在与否的返回值进行测试，以便筛选掉不支持双面打印的打印机。  
  
## 请参阅  
 <xref:System.Printing.PrintServer.GetPrintQueues%2A>   
 <xref:System.Printing.PrintServer>   
 <xref:System.Printing.LocalPrintServer>   
 <xref:System.Printing.EnumeratedPrintQueueTypes>   
 <xref:System.Printing.PrintQueue>   
 <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [Microsoft XPS Document Writer](http://go.microsoft.com/fwlink/?LinkId=147319)