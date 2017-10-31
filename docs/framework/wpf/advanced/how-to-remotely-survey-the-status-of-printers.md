---
title: "如何：远程调查打印机的状态 | Microsoft Docs"
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
  - "打印机状态, 远程调查"
  - "远程调查打印机状态"
  - "状态, 打印机, 远程调查"
  - "远程调查打印机状态"
ms.assetid: d6324759-8292-4c23-9584-9c708887dc94
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：远程调查打印机的状态
在任何给定时间，大中型公司都可能会有多台打印机由于夹纸、缺纸或者某种其他异常情况而无法工作。  [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)]的 [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] 中公开了一组丰富的打印机属性，通过这些属性可以快速调查打印机的状态。  
  
## 示例  
 下面是创建这种实用工具的主要步骤。  
  
1.  获取所有打印服务器的列表。  
  
2.  遍历各服务器以查询其打印队列。  
  
3.  在服务器遍历的每个处理过程中，遍历所有服务器的队列，并读取每个可能指示队列当前未工作的属性。  
  
 下面的代码由一系列代码段组成。  为简单起见，此示例假设存在一个用 CRLF 分隔的打印服务器列表。  变量 `fileOfPrintServers` 是该文件的一个 <xref:System.IO.StreamReader> 对象。  由于每个服务器名称都在其各自的行上，因此每次调用 <xref:System.IO.StreamReader.ReadLine%2A> 时都会获取下一台服务器的名称，并将 <xref:System.IO.StreamReader> 的游标移到下一行的开头。  
  
 在外部循环中，该代码为最后一台打印服务器创建一个 <xref:System.Printing.PrintServer> 对象，并指定该应用程序将对最后一台打印服务器具有管理权限。  
  
> [!NOTE]
>  如果存在多台服务器，则可以通过使用 [PrintServer\(String, String\<xref:System.Printing.PrintServer.%23ctor%28System.String%2CSystem.String%5B%5D%2CSystem.Printing.PrintSystemDesiredAccess%29> 构造函数来改进性能，这些构造函数仅对您将需要的属性进行初始化。  
  
 此示例随后使用 <xref:System.Printing.PrintServer.GetPrintQueues%2A> 来创建一个包含所有服务器队列的集合，并开始遍历它们。  内部循环包含一个与打印机状态的两种检查方法相对应的分支结构：  
  
-   您可以读取类型为 <xref:System.Printing.PrintQueueStatus> 的 <xref:System.Printing.PrintQueue.QueueStatus%2A> 属性的标志。  
  
-   您可以读取每个相关属性，如 <xref:System.Printing.PrintQueue.IsOutOfPaper%2A> 和 <xref:System.Printing.PrintQueue.IsPaperJammed%2A>。  
  
 此示例对这两种方法均进行了演示，因此用户在这之前会被询问要使用哪种方法，如果用户希望使用 <xref:System.Printing.PrintQueue.QueueStatus%2A> 属性的标志，则可以回答“y”（是）。  下面详细介绍了这两种方法。  
  
 最后，结果将呈现给用户。  
  
 [!code-cpp[PrinterStatusSurvey#SurveyQueues](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#surveyqueues)]
 [!code-csharp[PrinterStatusSurvey#SurveyQueues](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#surveyqueues)]
 [!code-vb[PrinterStatusSurvey#SurveyQueues](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#surveyqueues)]  
  
 若要使用 <xref:System.Printing.PrintQueue.QueueStatus%2A> 属性的标志来检查打印机状态，可以通过检查每个相关标志来查看它是否已经设置。  如需检查是否在一组位标志中设置了某个位，标准方法是将这组标志作为一个操作数，将需要检查的标志本身作为另一个操作数，对它们执行逻辑“与”运算。  由于该标志本身只设置了一个位，因此逻辑“与”运算的结果是至多设置了同一个位。  若要确定是否设置了该位，只需将逻辑“与”运算的结果与该标志本身进行比较。  有关更多信息，请参见 <xref:System.Printing.PrintQueueStatus>、[& 运算符（C\# 参考）](../Topic/&%20Operator%20\(C%23%20Reference\).md) 和 <xref:System.FlagsAttribute>。  
  
 对于每个设置了位的特性，该代码会在最终报告中添加一个将呈现给用户的通知  （下面将讨论在该代码末尾处调用的 **ReportAvailabilityAtThisTime** 方法）。  
  
 [!code-cpp[PrinterStatusSurvey#SpotTroubleUsingQueueAttributes](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#spottroubleusingqueueattributes)]
 [!code-csharp[PrinterStatusSurvey#SpotTroubleUsingQueueAttributes](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#spottroubleusingqueueattributes)]
 [!code-vb[PrinterStatusSurvey#SpotTroubleUsingQueueAttributes](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#spottroubleusingqueueattributes)]  
  
 若要使用每个属性来检查打印机状态，只需读取每个属性，如果该属性为 `true`，则在最终报告中添加一个将呈现给用户的说明  （下面将讨论在该代码末尾处调用的 **ReportAvailabilityAtThisTime** 方法）。  
  
 [!code-cpp[PrinterStatusSurvey#SpotTroubleUsingQueueProperties](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#spottroubleusingqueueproperties)]
 [!code-csharp[PrinterStatusSurvey#SpotTroubleUsingQueueProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#spottroubleusingqueueproperties)]
 [!code-vb[PrinterStatusSurvey#SpotTroubleUsingQueueProperties](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#spottroubleusingqueueproperties)]  
  
 创建 **ReportAvailabilityAtThisTime** 方法的目的在于让您确定队列在当前时间是否可用。  
  
 如果 <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> 属性和 <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> 属性相等，该方法将不执行任何操作；因为在这种情况下，打印机将一直可用。  如果这两个属性不同，则该方法将获取当前时间，当前时间随后将必须转换为自午夜以来的总分钟数，因为 <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> 属性和 <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> 属性是表示自午夜以来的总分钟数的 <xref:System.Int32> 值，而不是 <xref:System.DateTime> 对象。  最后，该方法将查看当前的时间是否介于开始时间和截止时间之间。  
  
 [!code-cpp[PrinterStatusSurvey#UsingStartAndUntilTimes](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#usingstartanduntiltimes)]
 [!code-csharp[PrinterStatusSurvey#UsingStartAndUntilTimes](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#usingstartanduntiltimes)]
 [!code-vb[PrinterStatusSurvey#UsingStartAndUntilTimes](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#usingstartanduntiltimes)]  
  
## 请参阅  
 <xref:System.Printing.PrintQueue.StartTimeOfDay%2A>   
 <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A>   
 <xref:System.DateTime>   
 <xref:System.Printing.PrintQueueStatus>   
 <xref:System.FlagsAttribute>   
 <xref:System.Printing.PrintServer.GetPrintQueues%2A>   
 <xref:System.Printing.PrintServer>   
 <xref:System.Printing.LocalPrintServer>   
 <xref:System.Printing.EnumeratedPrintQueueTypes>   
 <xref:System.Printing.PrintQueue>   
 [& 运算符（C\# 参考）](../Topic/&%20Operator%20\(C%23%20Reference\).md)   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)