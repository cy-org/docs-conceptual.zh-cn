---
title: "如何：确定此时是否可以打印一项打印作业 | Microsoft Docs"
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
  - "打印作业, 计时"
  - "打印队列, 计时"
  - "打印机, 可用性"
ms.assetid: 7e9c8ec1-abf6-4b3d-b1c6-33b35d3c4063
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：确定此时是否可以打印一项打印作业
打印队列并非一天 24 小时始终可用。  它们具有开始时间和结束时间的属性，可以对这些属性进行设置，使打印队列在一天的某些时间段不可用。  例如，您可以使用此功能将打印机预定为在下午 5 点以后只能由某个部门使用。  该部门将有一个队列使用打印机，该队列不同于其他部门的队列。  其他部门的队列将设置为在下午 5 点以后不可用，而支持的部门的队列可以设置为随时可以使用。  
  
 另外，打印作业本身可以设置为仅在指定的时段内是可打印的。  
  
 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)]的 [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] 中公开的 <xref:System.Printing.PrintQueue> 和 <xref:System.Printing.PrintSystemJobInfo> 类提供一种远程检查方式，用于检查给定的打印作业在当前时间是否可以在给定队列中打印。  
  
## 示例  
 下面的示例是一个可以诊断打印作业问题的示例。  
  
 下面是针对此类功能的两个主要步骤。  
  
1.  读取 <xref:System.Printing.PrintQueue> 的 <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> 和 <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> 属性，以确定当前时间是否介于这两个时间之间。  
  
2.  读取 <xref:System.Printing.PrintSystemJobInfo> 的 <xref:System.Printing.PrintSystemJobInfo.StartTimeOfDay%2A> 和 <xref:System.Printing.PrintSystemJobInfo.UntilTimeOfDay%2A> 属性，以确定当前时间是否介于这两个时间之间。  
  
 但是问题变复杂了，因为这些属性不是 <xref:System.DateTime> 对象，  而是 <xref:System.Int32> 对象，它们会将时间以午夜过后的分钟数表示。  另外，此处指的不是当前时区的午夜，而是 UTC（协调世界时）午夜。  
  
 第一个代码示例提供静态方法 **ReportQueueAndJobAvailability**，会为该方法传递一个 <xref:System.Printing.PrintSystemJobInfo>。该方法调用帮助器方法，以确定在当前时间是否可以打印该作业，如果不能，何时可以打印。  请注意，不会将 <xref:System.Printing.PrintQueue> 传递给该方法。  这是因为 <xref:System.Printing.PrintSystemJobInfo> 在其 <xref:System.Printing.PrintSystemJobInfo.HostingPrintQueue%2A> 属性中包括对队列的引用。  
  
 从属方法包括重载的 **ReportAvailabilityAtThisTime** 方法，它采用 <xref:System.Printing.PrintQueue> 或 <xref:System.Printing.PrintSystemJobInfo> 作为参数。  还存在一个 **TimeConverter.ConvertToLocalHumanReadableTime**。  下面将讨论上述所有方法。  
  
 **ReportQueueAndJobAvailability** 方法首先检查队列或打印作业在当前时间是否可用。  如果其中之一不可用，它将查看队列是否可用。  如果队列不可用，该方法将报告此事实以及队列将再次可用的时间。  然后，它检查作业，并查看其是否可用，随后报告可以打印作业的下一个时段。  最后，此方法报告可以打印作业的最早时间。  该时间是下列两个时间中较晚的一个时间。  
  
-   打印队列下次可用的时间。  
  
-   打印作业下次可用的时间。  
  
 当报告时间时，还会调用 <xref:System.DateTime.ToShortTimeString%2A> 方法，因为此方法会从输出中取消年、月和日的显示。  您不能将打印队列或打印作业的可用性限定为特定的年、月或日。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#reportqueueandjobavailability)]
 [!code-csharp[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#reportqueueandjobavailability)]
 [!code-vb[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#reportqueueandjobavailability)]  
  
 **ReportAvailabilityAtThisTime** 方法的两个重载是相同的（传递给它们的类型除外），所以下面仅给出 <xref:System.Printing.PrintQueue> 版本。  
  
> [!NOTE]
>  这些方法除类型外都相同，这就引出了这样一个问题，为什么这个示例不创建泛型方法 **ReportAvailabilityAtThisTime\<T\>**。  原因是这样一种方法将不得不限制为具有该方法调用的 **StartTimeOfDay** 和 **UntilTimeOfDay** 属性的类，但是泛型方法仅可以限制为单一类，并且继承树中 <xref:System.Printing.PrintQueue> 和 <xref:System.Printing.PrintSystemJobInfo> 的唯一共有类为 <xref:System.Printing.PrintSystemObject>，不具有上述属性。  
  
 **ReportAvailabilityAtThisTime** 方法（如下面的代码示例中所示）首先将 <xref:System.Boolean> sentinel 变量初始化为 `true`。  如果队列不可用，该变量将被重置为 `false`。  
  
 接下来，该方法将查看开始时间与“截止”时间是否相同。  如果相同，队列始终可用，所以该方法会返回 `true`。  
  
 如果队列始终不可用，该方法会使用静态 <xref:System.DateTime.UtcNow%2A> 属性将当前时间获取为 <xref:System.DateTime> 对象。  （我们不需要本地时间，因为 <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> 和 <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> 属性本身就是 UTC 时间。）  
  
 不过，这两个属性不是 <xref:System.DateTime> 对象，  它们是 <xref:System.Int32>，将时间表示为 UTC 午夜后的分钟数。  因此我们需要将 <xref:System.DateTime> 对象转换为午夜后的分钟数。  完成后，该方法将仅查看“当前”时间是否介于队列的开始时间和“截止”时间之间，如果“当前”时间未介于这两个时间之间，则将 sentinel 设置为 false，并返回 sentinel。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#PrintQueueStartUntil](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#printqueuestartuntil)]
 [!code-csharp[DiagnoseProblematicPrintJob#PrintQueueStartUntil](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#printqueuestartuntil)]
 [!code-vb[DiagnoseProblematicPrintJob#PrintQueueStartUntil](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#printqueuestartuntil)]  
  
 **TimeConverter.ConvertToLocalHumanReadableTime** 方法（如下面的代码示例中所示）不使用 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)]中引入的任何方法，所以下面将进行简单讨论。  该方法有一个双重转换的任务：它必须用一个表示午夜后分钟数的整数，并将其转换为用户可以理解的时间；同时必须将其转换为本地时间。  完成此任务的方法是：首先创建 <xref:System.DateTime> 对象（设置为午夜 UTC），然后使用 <xref:System.DateTime.AddMinutes%2A> 方法添加传递给该方法的分钟数。  这将返回一个新的 <xref:System.DateTime>，用以表示传递给该方法的初始时间。  然后，<xref:System.DateTime.ToLocalTime%2A> 方法将此时间转换为本地时间。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#TimeConverter](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#timeconverter)]
 [!code-csharp[DiagnoseProblematicPrintJob#TimeConverter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#timeconverter)]
 [!code-vb[DiagnoseProblematicPrintJob#TimeConverter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#timeconverter)]  
  
## 请参阅  
 <xref:System.DateTime>   
 <xref:System.Printing.PrintSystemJobInfo>   
 <xref:System.Printing.PrintQueue>   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)