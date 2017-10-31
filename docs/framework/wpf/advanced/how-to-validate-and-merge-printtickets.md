---
title: "如何：验证和合并 PrintTicket | Microsoft Docs"
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
  - "合并 PrintTicket"
  - "PrintTicket, 合并"
  - "PrintTicket, 验证"
  - "PrintTicket 验证"
ms.assetid: 4fe2d501-d0b0-4fef-86af-6ffe6c162532
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：验证和合并 PrintTicket
[!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] [Print Schema](http://go.microsoft.com/fwlink/?LinkId=186397)（打印架构）包含灵活且可扩展的 <xref:System.Printing.PrintCapabilities> 和 <xref:System.Printing.PrintTicket> 元素。  前者可以详细列举打印设备的功能，后者用于指定该设备应该如何使用这些功能来处理特定文档序列、单个文档或单个页面。  
  
 支持打印的应用程序的典型任务序列如下所示：  
  
1.  确定打印机的功能。  
  
2.  配置 <xref:System.Printing.PrintTicket> 以使用这些功能。  
  
3.  验证 <xref:System.Printing.PrintTicket>。  
  
 本文演示如何进行以上操作。  
  
## 示例  
 在下面的简单示例中，我们只关注打印机是否支持双面打印。  主要步骤如下所示。  
  
1.  使用 <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A> 方法获取 <xref:System.Printing.PrintCapabilities> 对象。  
  
2.  测试是否存在所需的功能。  在下面的示例中，我们测试 <xref:System.Printing.PrintCapabilities> 对象的 <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> 属性，验证是否能够使用“页面翻转”沿页面长边在一页纸的双面进行打印。  因为 <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> 是一个集合，所以我们使用 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 的 `Contains` 方法。  
  
    > [!NOTE]
    >  此步骤不是必需的。  下面使用的 <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> 方法将针对打印机的功能检测 <xref:System.Printing.PrintTicket> 中的每个请求。  如果打印机不支持请求的功能，则打印机驱动程序将替换为该方法返回的 <xref:System.Printing.PrintTicket> 中的另一个请求。  
  
3.  如果打印机支持双面打印，则代码示例会创建请求双面打印的 <xref:System.Printing.PrintTicket>。  但是应用程序不会指定 <xref:System.Printing.PrintTicket> 元素中提供的每个可能的打印机设置。  这将浪费程序员时间和程序时间。  代码仅设置双面打印请求，然后将此 <xref:System.Printing.PrintTicket> 与现有的、完全配置且经过验证的 <xref:System.Printing.PrintTicket>（在此例中，是用户的默认 <xref:System.Printing.PrintTicket>）进行合并。  
  
4.  相应地，本示例调用 <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> 方法将最小的新 <xref:System.Printing.PrintTicket> 与用户的默认 <xref:System.Printing.PrintTicket> 合并。  这会返回 <xref:System.Printing.ValidationResult>，它包含新 <xref:System.Printing.PrintTicket> 作为其属性之一。  
  
5.  然后代码会测试新 <xref:System.Printing.PrintTicket> 是否请求双面打印。  如果它请求双面打印，那么代码会将其作为用户的新默认打印票证。  如果没有执行上述步骤 2，并且打印机不支持沿长边进行双面打印，则测试将导致 `false`。  （请参见上述“注意”部分。）  
  
6.  最后一个重要步骤是使用 <xref:System.Printing.PrintQueue.Commit%2A> 方法提交对 <xref:System.Printing.PrintQueue> 的 <xref:System.Printing.PrintQueue.UserPrintTicket%2A> 属性的更改。  
  
 [!code-csharp[PrintTicketManagment#UsingMergeAndValidate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#usingmergeandvalidate)]
 [!code-vb[PrintTicketManagment#UsingMergeAndValidate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#usingmergeandvalidate)]  
  
 在下面显示了代码的剩余部分，以便于您能快速测试本示例。  创建项目和命名空间，然后将本文中的两个代码段粘贴到命名空间块中。  
  
 [!code-csharp[PrintTicketManagment#UIForMergeAndValidatePTUtility](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#uiformergeandvalidateptutility)]
 [!code-vb[PrintTicketManagment#UIForMergeAndValidatePTUtility](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#uiformergeandvalidateptutility)]  
  
## 请参阅  
 <xref:System.Printing.PrintCapabilities>   
 <xref:System.Printing.PrintTicket>   
 <xref:System.Printing.PrintServer.GetPrintQueues%2A>   
 <xref:System.Printing.PrintServer>   
 <xref:System.Printing.EnumeratedPrintQueueTypes>   
 <xref:System.Printing.PrintQueue>   
 <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [Print Schema](http://go.microsoft.com/fwlink/?LinkId=186397)