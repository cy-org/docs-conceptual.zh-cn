---
title: "如何：对 Windows 窗体控件进行线程安全调用 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "EHInvalidOperation.WinForms.IllegalCrossThreadCall"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "线程安全性, 调用控件 [Windows 窗体]"
  - "调用控件, 线程安全性 [Windows 窗体]"
  - "CheckForIllegalCrossThreadCalls 属性 [Windows 窗体]"
  - "Windows 窗体控件, 多线程处理"
  - "BackgroundWorker 类, 示例"
  - "线程处理 [Windows 窗体], 跨线程调用"
  - "控件 [Windows 窗体], 多线程处理"
ms.assetid: 138f38b6-1099-4fd5-910c-390b41cbad35
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：对 Windows 窗体控件进行线程安全调用
如果使用多线程处理来提高 Windows 窗体应用程序的性能，则你必须确保以线程安全的方式调用控件。  
  
 访问 Windows 窗体控件不是本身就线程安全的。 如果有两个或两个以上线程操作控件的状态，则可能迫使该控件处于不一致状态。 可能出现其他与线程相关的 bug，例如争用条件和死锁。 请务必确保以线程安全的方式访问控件。  
  
 从未使用 <xref:System.Windows.Forms.Control.Invoke%2A> 方法创建控件的线程调用控件是不安全的。 下面是一个非线程安全的调用示例。  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#6](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#6)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#6)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#6)]  
  
 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 可帮助检测你是否以线程安全的方式访问控件。 在调试器中运行应用程序并且未创建控件的线程试图调用控件时，调试器会引发 <xref:System.InvalidOperationException> 消息，“从并未创建该控件的线程访问该控件 *控件名称*”。  
  
 在调试过程中、在某些情况下以及在运行时均极有可能发生此异常。 当你调试在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 之前用 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 编写的应用程序时可能会看到此异常。 强烈建议你在遇到此问题时修复它，但你可通过将 <xref:System.Windows.Forms.Control.CheckForIllegalCrossThreadCalls%2A> 属性设置为 `false` 来禁用它。 这使控件可像在 Visual Studio .NET 2003 和 [!INCLUDE[net_v11_short](../../../../includes/net-v11-short-md.md)] 下那样运行。  
  
> [!NOTE]
>  如果你使用的是窗体上的 ActiveX 控件，则在调试器下运行时可能会收到跨线程 <xref:System.InvalidOperationException>。 发生此情况时，ActiveX 控件不支持多线程处理。 有关在 Windows 窗体中使用 ActiveX 控件的详细信息，请参阅 [Windows 窗体和非托管应用程序](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md)。 如果你使用的是 Visual Studio，则可通过禁用 Visual Studio 的宿主进程来避免此异常，请参阅[如何：禁用承载进程](../Topic/How%20to:%20Disable%20the%20Hosting%20Process.md)。  
  
## 对 Windows 窗体控件进行线程安全的调用  
  
#### 如需对 Windows 窗体控件进行线程安全的调用  
  
1.  查询控件的 <xref:System.Windows.Forms.Control.InvokeRequired%2A> 属性。  
  
2.  若 <xref:System.Windows.Forms.Control.InvokeRequired%2A> 返回 `true`，则用实际调用控件的委托来调用 <xref:System.Windows.Forms.Control.Invoke%2A>。  
  
3.  若 <xref:System.Windows.Forms.Control.InvokeRequired%2A> 返回 `false`，则请直接调用控件。  
  
 在以下代码示例中，在 `ThreadProcSafe` 方法中实现了线程安全的调用，该方法由后台线程执行。 若 <xref:System.Windows.Forms.TextBox> 控件的 <xref:System.Windows.Forms.Control.InvokeRequired%2A> 返回 `true`，则 `ThreadProcSafe` 方法创建一个 `SetTextCallback` 实例并将其传递到窗体的 <xref:System.Windows.Forms.Control.Invoke%2A> 方法。 这导致在创建了 `SetText` 控件的线程上调用 <xref:System.Windows.Forms.TextBox> 方法，并且在该线程上下文中直接设置 <xref:System.Windows.Forms.Control.Text%2A> 属性。  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#7](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#7)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#7)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#7)]  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#3](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#3)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#3)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#3)]  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#8](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#8)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#8](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#8)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#8](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#8)]  
  
## 通过使用 BackgroundWorker 进行线程安全的调用  
 在应用程序中实现多线程的首选方式是使用 <xref:System.ComponentModel.BackgroundWorker> 组件。<xref:System.ComponentModel.BackgroundWorker> 组件为多线程处理使用事件驱动模型。 后台线程运行你的 <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序，创建了你的控件的线程运行 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 和 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件处理程序。 你可以从 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 和 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件处理器中调用控件。  
  
#### 如需通过使用 BackgroundWorker 进行线程安全的调用  
  
1.  创建一种方法来进行你想在后台线程中进行的工作。 不要调用由此方法中的主线程所创建的控件。  
  
2.  创建一种方法来报告后台工作结束后的后台工作结果。 你可以调用由此方法中的主线程所创建的控件。  
  
3.  将步骤 1 中创建的方法绑定到 <xref:System.ComponentModel.BackgroundWorker.DoWork> 实例中的 <xref:System.ComponentModel.BackgroundWorker> 事件，并将步骤 2 中创建的方法绑定到同一实例的 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件。  
  
4.  若要启动后台线程，请调用 <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> 实例的 <xref:System.ComponentModel.BackgroundWorker> 方法。  
  
 在以下代码示例中，<xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序使用 <xref:System.Threading.Thread.Sleep%2A> 来模拟需要花费一些时间的工作。 它不会调用该窗体的 <xref:System.Windows.Forms.TextBox> 控件。<xref:System.Windows.Forms.TextBox> 控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性直接在 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件处理程序中设置。  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#5](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#5)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#5)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#5)]  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#9](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#9)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#9](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#9)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#9](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#9)]  
  
 也可通过使用 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件来报告后台任务的进度。 如需包含该事件的示例，请参阅 <xref:System.ComponentModel.BackgroundWorker>。  
  
## 示例  
 以下代码示例是一个完整的 Windows 窗体应用程序，由带有三个按钮和一个文本框的窗体组成。 第一个按钮演示了不安全的跨线程访问，第二个按钮使用 <xref:System.Windows.Forms.Control.Invoke%2A> 演示了安全的访问，第三个按钮通过使用 <xref:System.ComponentModel.BackgroundWorker> 演示了安全的访问。  
  
> [!NOTE]
>  有关如何运行此示例的说明，请参阅[How to: Compile and Run a Complete Windows Forms Code Example Using Visual Studio](http://msdn.microsoft.com/zh-cn/cc447f7e-4c3b-4397-9d05-aeba3ca49416)。 该示例需引用 System.Drawing 和 System.Windows.Forms 程序集。  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#1)]  
  
 运行应用程序并单击“不安全调用”按钮时，你可以立即在文本框中看到“由主线程写入”。 两秒钟之后，尝试进行不安全调用时，Visual Studio 调试器指示发生了异常。 调试器在后台线程中试图直接写入文本框的那一行停止。 你将必须重新启动该应用程序来测试其他两个按钮。 单击“安全调用”按钮时，文本框中显示“由主线程写入”。 两秒钟之后，文本框中被设置为“由后台线程写入 \(Invoke\)”，表示调用了 <xref:System.Windows.Forms.Control.Invoke%2A> 方法。 单击“安全 BW 调用”按钮时，文本框中显示“由主线程写入”。 两秒钟之后，文本框被设置为“在后台线程完成后由主线程写入”，表示调用了 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 的 <xref:System.ComponentModel.BackgroundWorker> 事件的处理程序。  
  
## 可靠编程  
  
> [!CAUTION]
>  使用任何种类的多线程时，都有可能会遇到非常严重且复杂的 bug。 有关详细信息，请在实现使用多线程处理的任何解决方案之前参阅[Managed Threading Best Practices](../../../../docs/standard/threading/managed-threading-best-practices.md)。  
  
## 请参阅  
 <xref:System.ComponentModel.BackgroundWorker>   
 [如何：在后台运行操作](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [如何：实现使用后台操作的窗体](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [使用 .NET Framework 开发自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [Windows 窗体和非托管应用程序](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md)