---
title: "How to: Use Components That Support the Event-based Asynchronous Pattern | Microsoft Docs"
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
  - "Event-based Asynchronous Pattern"
  - "ProgressChangedEventArgs class"
  - "BackgroundWorker component"
  - "events [.NET Framework], asynchronous"
  - "Asynchronous Pattern"
  - "AsyncOperationManager class"
  - "threading [.NET Framework], asynchronous features"
  - "components [.NET Framework], asynchronous"
  - "AsyncOperation class"
  - "threading [Windows Forms], asynchronous features"
  - "AsyncCompletedEventArgs class"
ms.assetid: 35e9549c-1568-4768-ad07-17cc6dff11e1
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# How to: Use Components That Support the Event-based Asynchronous Pattern
很多组件都提供了异步执行工作的选项。  例如，使用 <xref:System.Media.SoundPlayer> 和 <xref:System.Windows.Forms.PictureBox> 组件，您可以“在后台”加载声音和图像，主线程则继续运行而不会中断。  
  
 使用支持[Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)的类上的异步方法就像将事件处理程序附加到组件的 *方法名称MethodName*`Completed` 事件一样简单，这与处理任何其他事件完全一样。  当您调用 *方法名称MethodName*`Async 方法时，您的应用程序将继续运行而不会中断，直到引发` 方法名称*MethodName*`Completed` 事件才会停止。  在您的事件处理程序中，您可以检查 <xref:System.ComponentModel.AsyncCompletedEventArgs> 参数来确定异步操作是已经成功完成，还是被取消了。  
  
 有关使用事件处理程序的更多信息，请参见 [事件处理程序概述](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)。  
  
 下面的过程演示如何使用 <xref:System.Windows.Forms.PictureBox> 控件的异步图像加载功能。  
  
### 使 PictureBox 控件异步加载图像  
  
1.  在窗体中创建 <xref:System.Windows.Forms.PictureBox> 组件的一个实例。  
  
2.  给 <xref:System.Windows.Forms.PictureBox.LoadCompleted> 事件分配一个事件处理程序。  
  
     在此处检查异步下载过程中是否发生了任何错误，  此处还可以检查是否取消了操作。  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#2)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#5)]  
  
3.  向窗体添加两个按钮，名称分别是 `loadButton` 和 `cancelLoadButton`。  添加 <xref:System.Windows.Forms.Control.Click> 事件处理程序，用于开始和取消下载。  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#4)]  
  
4.  运行应用程序。  
  
     在图像下载过程中，您可以自由移动窗体、最小化窗体和最大化窗体。  
  
## 请参阅  
 [如何：在后台运行操作](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)   
 [NOT IN BUILD: Multithreading in Visual Basic](http://msdn.microsoft.com/zh-cn/c731a50c-09c1-4468-9646-54c86b75d269)