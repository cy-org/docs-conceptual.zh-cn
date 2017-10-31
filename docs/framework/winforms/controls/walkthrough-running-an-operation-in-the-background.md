---
title: "演练：在后台运行操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "后台操作"
  - "背景任务"
  - "后台线程"
  - "BackgroundWorker 类, 示例"
  - "窗体, 后台操作"
  - "窗体, 多线程处理"
  - "线程处理 [Windows 窗体], 后台操作"
ms.assetid: 1b9a4e0a-f134-48ff-a1be-c461446a31ba
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 演练：在后台运行操作
如果有一个需要很长时间才能完成的操作，而且不希望用户界面中出现延迟，则可以使用 <xref:System.ComponentModel.BackgroundWorker> 类来在另一个线程上运行该操作。  
  
 有关此示例中所用代码的完整清单，请参见 [如何：在后台运行操作](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在后台运行操作  
  
1.  当窗体在 Windows 窗体设计器中处于活动状态时，将两个 <xref:System.Windows.Forms.Button> 控件从**“工具箱”**拖动到窗体中，然后根据下表设置这两个按钮的 `Name` 和 <xref:System.Windows.Forms.Control.Text%2A> 属性。  
  
    |Button|名称|Text|  
    |------------|--------|----------|  
    |`button1`|`startBtn`|Start|  
    |`button2`|`cancelBtn`|取消|  
  
2.  打开**“工具箱”**，单击**“组件”**选项卡，然后将 <xref:System.ComponentModel.BackgroundWorker> 组件拖动到窗体上。  
  
     `backgroundWorker1` 组件显示在**“组件栏”**中。  
  
3.  在**“属性”**窗口中，将 <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> 属性设置为 `true`。  
  
4.  在**“属性”**窗口中，单击**“事件”**按钮，然后双击 <xref:System.ComponentModel.BackgroundWorker.DoWork> 和 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件以创建事件处理程序。  
  
5.  将耗时的代码插入到 <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序中。  
  
6.  从 <xref:System.ComponentModel.DoWorkEventArgs> 参数的 <xref:System.ComponentModel.DoWorkEventArgs.Argument%2A> 属性中提取该操作所需的所有参数。  
  
7.  将计算的结果赋给 <xref:System.ComponentModel.DoWorkEventArgs> 的 <xref:System.ComponentModel.DoWorkEventArgs.Result%2A> 属性。  
  
     计算结果可供 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件处理程序使用。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#2)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#2)]  
  
8.  在 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件处理程序中，插入用来检索操作结果的代码。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#3)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#3)]  
  
9. 实现 `TimeConsumingOperation` 方法。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#4)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#4)]  
  
10. 在 Windows 窗体设计器中双击 `startButton`，创建新的 <xref:System.Windows.Forms.Control.Click> 事件处理程序。  
  
11. 在 `startButton` 的 <xref:System.Windows.Forms.Control.Click> 事件处理程序中，调用 <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> 方法。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#5)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#5)]  
  
12. 在 Windows 窗体设计器中双击 `cancelButton`，创建新的 <xref:System.Windows.Forms.Control.Click> 事件处理程序。  
  
13. 在 `cancelButton` 的 <xref:System.Windows.Forms.Control.Click> 事件处理程序中，调用 <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> 方法。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#6)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#6)]  
  
14. 在文件的顶部，导入 System.ComponentModel 和 System.Threading 命名空间。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#7)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#7)]  
  
15. 按 F6 生成解决方案，然后按 Ctrl\-F5 在调试器外部运行该应用程序。  
  
> [!NOTE]
>  如果按 F5 在调试器中运行应用程序，则调试器将捕捉和显示在 `TimeConsumingOperation` 方法中引发的异常。  当在调试器外部运行应用程序时，<xref:System.ComponentModel.BackgroundWorker> 将处理该异常并将其缓存在 <xref:System.ComponentModel.RunWorkerCompletedEventArgs> 的 <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A> 属性中。  
  
1.  单击**“启动”**按钮运行异步操作，然后单击**“取消”**按钮停止正在运行的异步操作。  
  
     每个操作的结果均在 <xref:System.Windows.Forms.MessageBox> 中显示。  
  
## 后续步骤  
  
-   实现一个该窗体，该窗体随着异步操作的进行报告进度。  有关更多信息，请参见 [如何：实现使用后台操作的窗体](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)。  
  
-   实现支持组件异步模式的类。  有关更多信息，请参见 [Implementing the Event\-based Asynchronous Pattern](../../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)。  
  
## 请参阅  
 <xref:System.ComponentModel.BackgroundWorker>   
 <xref:System.ComponentModel.DoWorkEventArgs>   
 [如何：实现使用后台操作的窗体](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [如何：在后台运行操作](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [BackgroundWorker 组件](../../../../docs/framework/winforms/controls/backgroundworker-component.md)