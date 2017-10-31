---
title: "微调异步应用程序 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 4c3e7997-a95f-4fbe-a6ac-60ba042d30b9
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 7d0cac2fe7305031b93a375a08e785285a291320
ms.lasthandoff: 03/13/2017

---
# <a name="fine-tuning-your-async-application-visual-basic"></a>微调异步应用程序 (Visual Basic)
您可以添加精度和灵活性异步应用程序使用的方法和属性，<xref:System.Threading.Tasks.Task>类型提供。</xref:System.Threading.Tasks.Task> 本部分中的主题说明使用示例，<xref:System.Threading.CancellationToken>和重要`Task`方法如<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>和<xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName>。</xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName> </xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> </xref:System.Threading.CancellationToken>  
  
 通过使用`WhenAny`和`WhenAll`，可以更轻松地启动多个任务并等待其完成通过监视单个任务。  
  
-   `WhenAny`返回集合中的任何任务完成后完成的任务。  
  
     有关示例，请使用`WhenAny`，请参阅[一个是否已完成 (Visual Basic 中) 后取消剩余异步任务](../../../../visual-basic/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md)和[启动多个异步任务和过程它们为它们全部 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md)。  
  
-   `WhenAll`返回在集合中的所有任务都都已完成时完成的任务。  
  
     有关详细信息和使用的示例， `WhenAll`，请参阅[如何︰ 扩展异步演练使用 Task.WhenAll (Visual Basic 中) 通过](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)。  
  
 本部分包括下面的示例。  
  
-   [取消一个异步任务或一组任务 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/async/cancel-an-async-task-or-a-list-of-tasks.md)。  
  
-   [在一段时间 (Visual Basic 中) 后取消异步任务](../../../../visual-basic/programming-guide/concepts/async/cancel-async-tasks-after-a-period-of-time.md)  
  
-   [异步任务取消剩余一个后完成 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md)  
  
-   [启动多个异步任务并在其完成 (Visual Basic 中) 时处理](../../../../visual-basic/programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md)  
  
> [!NOTE]
>  若要运行的示例，必须具有 Visual Studio 2012 或更高版本和.NET Framework 4.5 或更高版本安装在您的计算机上。  
  
 项目创建一个 UI，其中包含一个按钮用于启动进程和取消与下图显示的按钮。 这些按钮被命名为`startButton`和`cancelButton`。  
  
 ![WPF 窗口与取消按钮](../../../../csharp/programming-guide/concepts/async/media/cancellation.png "取消")  
  
 您可以下载完整的 Windows Presentation Foundation (WPF) 项目，从[异步示例︰ 精细优化您的应用程序](http://go.microsoft.com/fwlink/?LinkId=255046)。  
  
## <a name="see-also"></a>另请参阅  
 [异步编程使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)
