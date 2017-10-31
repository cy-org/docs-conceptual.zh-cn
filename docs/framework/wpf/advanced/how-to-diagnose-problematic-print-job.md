---
title: "如何：诊断有问题的打印作业 | Microsoft Docs"
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
  - "打印作业, 诊断问题"
  - "打印作业, 疑难解答"
  - "打印作业问题疑难解答"
ms.assetid: b081a170-84c6-48f9-a487-5766a8d58a82
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：诊断有问题的打印作业
网络管理员经常听到用户抱怨打印作业不打印或打印速度慢。  [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)]的 [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] 中公开了一组丰富的打印作业属性，通过这些属性可以快速地对打印作业进行远程诊断。  
  
## 示例  
 下面是创建这种实用工具的主要步骤。  
  
1.  识别用户正在抱怨的打印作业。  用户通常不能准确地完成此步骤。  他们可能不知道打印服务器或打印机的名称。  用户可能不是使用设置打印机的 <xref:System.Printing.PrintQueue.Location%2A> 属性时所使用的术语来描述打印机的位置。  因此，最好是生成用户当前提交作业的列表。  如果有多个作业，则可以通过用户与打印系统管理员之间的通信来查明有问题的作业。  具体步骤如下。  
  
    1.  获取所有打印服务器的列表。  
  
    2.  遍历各服务器以查询其打印队列。  
  
    3.  在服务器遍历的每个处理过程中，遍历服务器的所有队列以查询其作业。  
  
    4.  在队列遍历的每个阶段，遍历其作业并收集与提出问题的用户所提交的作业有关的标识信息。  
  
2.  识别出有问题的打印作业之后，检查相关的属性以查明可能的问题所在。  例如，问题是由于打印作业处于错误状态引起的？还是由于处理队列的打印机在执行打印作业之前进入脱机状态而引起的？  
  
 下面的代码由一系列代码示例组成。  第一个代码示例包含打印队列的遍历  （上述步骤 1c）。变量 `myPrintQueues` 是当前打印服务器的 <xref:System.Printing.PrintQueueCollection> 对象。  
  
 代码示例首先使用 <xref:System.Printing.PrintQueue.Refresh%2A?displayProperty=fullName> 刷新当前打印队列对象。  这可以确保此对象的属性准确地表示所代表的物理打印机的状态。  然后，应用程序使用 <xref:System.Printing.PrintQueue.GetPrintJobInfoCollection%2A> 获取该打印队列中当前所包含的打印作业的集合。  
  
 下一步，应用程序遍历 <xref:System.Printing.PrintSystemJobInfo> 集合，并将各 <xref:System.Printing.PrintSystemJobInfo.Submitter%2A> 属性与提出问题的用户的别名进行比较。  如果两者匹配，则应用程序将与作业有关的标识信息添加到将显示的字符串中  （`userName` 和 `jobList` 变量之前已在应用程序中初始化）。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#enumeratejobsinqueues)]
 [!code-csharp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#enumeratejobsinqueues)]
 [!code-vb[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#enumeratejobsinqueues)]  
  
 下面的代码示例使用步骤 2 中的应用程序  （如上所示）。已识别出有问题的作业，应用程序提示输入标识此作业的信息。  根据此信息创建 <xref:System.Printing.PrintServer>、<xref:System.Printing.PrintQueue> 和 <xref:System.Printing.PrintSystemJobInfo> 对象。  
  
 此时，应用程序包含一个与检查打印作业的状态的两种方法相对应的分支结构：  
  
-   您可以读取类型为 <xref:System.Printing.PrintJobStatus> 的 <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> 属性的标志。  
  
-   也可以读取每个相关属性，如 <xref:System.Printing.PrintSystemJobInfo.IsBlocked%2A> 和 <xref:System.Printing.PrintSystemJobInfo.IsInError%2A>。  
  
 此示例对这两种方法均进行了演示，因此用户在这之前会被提示选择要使用哪种方法，如果希望使用 <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> 属性的标志，则回答“Y”。  下面详细介绍了这两种方法。  最后，应用程序使用名为 **ReportQueueAndJobAvailability** 的方法来报告此时是否可以打印该作业。  [确定此时是否可以打印一项打印作业](../../../../docs/framework/wpf/advanced/how-to-discover-whether-a-print-job-can-be-printed-at-this-time-of-day.md)中对这一方法进行了讨论。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#identifyanddiagnoseproblematicjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#identifyanddiagnoseproblematicjob)]
 [!code-vb[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#identifyanddiagnoseproblematicjob)]  
  
 要使用 <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> 属性的标志来检查打印作业状态，可以检查每个相关标志来查看它是否已设置。  如需检查是否在一组位标志中设置了某个位，标准方法是将这组标志作为一个操作数，将需要检查的标志本身作为另一个操作数，对它们执行逻辑“与”运算。  由于该标志本身只设置了一个位，因此逻辑“与”运算的结果是至多设置了同一个位。  若要确定是否设置了该位，只需将逻辑“与”运算的结果与该标志本身进行比较。  有关更多信息，请参见 <xref:System.Printing.PrintJobStatus>、[& 运算符（C\# 参考）](../Topic/&%20Operator%20\(C%23%20Reference\).md)和 <xref:System.FlagsAttribute>。  
  
 对于已设置位的每个特性，代码都会将其报告给控制台屏幕，有时还建议应对的方法  （暂停作业或队列时调用的 **HandlePausedJob** 方法在下面讨论）。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobattributes)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobattributes)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobattributes)]  
  
 要使用单独的属性检查打印作业状态，只需读取各属性。如果属性为 `true`，则报告给控制台屏幕并且可能会建议应对的方法  （暂停作业或队列时调用的 **HandlePausedJob** 方法在下面讨论）。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobproperties)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobproperties)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobproperties)]  
  
 使用 **HandlePausedJob** 方法，应用程序用户可以远程继续暂停的作业。  因为暂停此打印队列可能有充分的理由，所以此方法开始时会提示用户决定是否继续。  如果回答“Y”，则调用 <xref:System.Printing.PrintQueue.Resume%2A?displayProperty=fullName> 方法。  
  
 接下来提示用户决定是否继续执行作业本身（只有当它是独立于打印队列而暂停的时，才会出现此提示。  这可通过将 <xref:System.Printing.PrintQueue.IsPaused%2A?displayProperty=fullName> 和 <xref:System.Printing.PrintSystemJobInfo.IsPaused%2A?displayProperty=fullName> 进行比较来判断）。如果回答“Y”，则调用 <xref:System.Printing.PrintSystemJobInfo.Resume%2A?displayProperty=fullName> 方法；否则，调用 <xref:System.Printing.PrintSystemJobInfo.Cancel%2A>。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#HandlePausedJob](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#handlepausedjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#HandlePausedJob](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#handlepausedjob)]
 [!code-vb[DiagnoseProblematicPrintJob#HandlePausedJob](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#handlepausedjob)]  
  
## 请参阅  
 <xref:System.Printing.PrintJobStatus>   
 <xref:System.Printing.PrintSystemJobInfo>   
 <xref:System.FlagsAttribute>   
 <xref:System.Printing.PrintQueue>   
 [& 运算符（C\# 参考）](../Topic/&%20Operator%20\(C%23%20Reference\).md)   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)