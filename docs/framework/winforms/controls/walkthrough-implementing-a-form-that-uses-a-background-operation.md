---
title: "演练：实现一个使用后台操作的窗体 | Microsoft Docs"
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
  - "BackgroundWorker 组件"
  - "窗体, 后台操作"
  - "窗体, 多线程处理"
  - "线程处理 [Windows 窗体], 后台操作"
  - "线程处理 [Windows 窗体], 窗体"
  - "线程处理 [Windows 窗体], 演练"
ms.assetid: 4691b796-9200-471a-89c3-ba4c7cc78c03
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# 演练：实现一个使用后台操作的窗体
如果某项操作需要很长的时间才能完成，并且不希望用户界面 \(UI\) 停止响应或“挂起”，则可以使用 <xref:System.ComponentModel.BackgroundWorker> 类在另一个线程中执行这种操作。  
  
 本演练演示如何使用 <xref:System.ComponentModel.BackgroundWorker> 类来在“后台”执行耗时的计算，同时用户界面保持响应。  演练时，将有一个异步计算斐波那契数列的应用程序。  即使计算很大的斐波那契数列需要花费大量的时间，但主 UI 线程不会被这种延时中断，并且在计算期间窗体仍会响应。  
  
 本演练涉及以下任务：  
  
-   创建一个基于 Windows 的应用程序  
  
-   在窗体中创建一个 <xref:System.ComponentModel.BackgroundWorker>  
  
-   添加异步事件处理程序  
  
-   添加进度报告和取消支持  
  
 要获得此示例中使用的代码的完整清单，请参见 [如何：实现使用后台操作的窗体](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 第一步是创建项目并设置窗体。  
  
#### 创建使用后台操作的窗体  
  
1.  创建一个名为 `BackgroundWorkerExample` 的基于 Windows 的应用程序项目。  有关详细信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  在**“解决方案资源管理器”**中，右击**“Form1”**，然后从快捷菜单中选择**“重命名”**。  将文件名更改为 `FibonacciCalculator`。  当询问是否希望重命名对代码元素“`Form1`”的所有引用时，单击**“是”**按钮。  
  
3.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.NumericUpDown> 控件拖到窗体上。  将 <xref:System.Windows.Forms.NumericUpDown.Minimum%2A> 属性设置为 `1` 而 <xref:System.Windows.Forms.NumericUpDown.Maximum%2A> 属性设置为 `91`。  
  
4.  向窗体添加两个 <xref:System.Windows.Forms.Button> 控件。  
  
5.  将第一个 <xref:System.Windows.Forms.Button> 控件重命名为 `startAsyncButton`，并将 <xref:System.Windows.Forms.Control.Text%2A> 属性设置为 `Start Async`。  将第二个 <xref:System.Windows.Forms.Button> 控件重命名为 `cancelAsyncButton`，并将 <xref:System.Windows.Forms.Control.Text%2A> 属性设置为 `Cancel Async`。  将 <xref:System.Windows.Forms.Control.Enabled%2A> 属性设置为 `false`。  
  
6.  为两个 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件创建事件处理程序。  有关详细信息，请参见 [How to: Create Event Handlers Using the Designer](http://msdn.microsoft.com/zh-cn/8461e9b8-14e8-406f-936e-3726732b23d2)。  
  
7.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Label> 控件拖到窗体上并将它重命名为 `resultLabel`。  
  
8.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.ProgressBar> 控件拖到窗体上。  
  
## 在窗体中创建一个 BackgroundWorker  
 可以利用**“Windows 窗体设计器”**为异步操作创建 <xref:System.ComponentModel.BackgroundWorker>。  
  
#### 利用设计器创建一个 BackgroundWorker  
  
-   从**“工具箱”**的**“组件”**选项卡中，将一个 <xref:System.ComponentModel.BackgroundWorker> 拖动到窗体上。  
  
## 添加异步事件处理程序  
 现在已准备好为 <xref:System.ComponentModel.BackgroundWorker> 组件的异步事件添加事件处理程序。  这些事件处理程序将调用在后台运行的计算斐波那契数列的耗时操作。  
  
#### 实现异步事件处理程序  
  
1.  在**“属性”**窗口中的 <xref:System.ComponentModel.BackgroundWorker> 组件仍处于选中状态时，单击**“事件”**按钮。  双击 <xref:System.ComponentModel.BackgroundWorker.DoWork> 和 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件来创建事件处理程序。  有关如何使用事件处理程序的更多信息，请参见[How to: Create Event Handlers Using the Designer](http://msdn.microsoft.com/zh-cn/8461e9b8-14e8-406f-936e-3726732b23d2)。  
  
2.  在窗体中创建一个称为 `ComputeFibonacci` 的新方法。  此方法完成实际的工作，并在后台运行。  这些代码演示了斐波那契数列算法的递归实现，这种算法的效率非常低，对于较大的数值花费的时间按指数增长。  在这里使用是出于演示的目的，为了说明在应用程序中某项操作可能带来长时间的延迟。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#10](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#10)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#10)]
     [!code-vb[System.ComponentModel.BackgroundWorker#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#10)]  
  
3.  在 <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序中，添加对 `ComputeFibonacci` 方法的调用。  将 <xref:System.ComponentModel.DoWorkEventArgs> 的 <xref:System.ComponentModel.DoWorkEventArgs.Argument%2A> 属性作为 `ComputeFibonacci` 的第一个参数。  稍后将 <xref:System.ComponentModel.BackgroundWorker> 和 <xref:System.ComponentModel.DoWorkEventArgs> 参数用于进度报告和取消支持。  将 `ComputeFibonacci` 的返回值赋给 <xref:System.ComponentModel.DoWorkEventArgs> 的 <xref:System.ComponentModel.DoWorkEventArgs.Result%2A> 属性。  <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件处理程序可以使用此结果。  
  
    > [!NOTE]
    >  <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序不直接引用 `backgroundWorker1` 实例变量，因为这将会使此事件处理程序和某个特定的 <xref:System.ComponentModel.BackgroundWorker> 实例耦合。  相反，引发此事件的 <xref:System.ComponentModel.BackgroundWorker> 引用将从 `sender` 参数恢复。  当窗体承载多个 <xref:System.ComponentModel.BackgroundWorker> 时这非常重要。  在 <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序中不操作任何用户界面对象也非常重要。  而应该通过 <xref:System.ComponentModel.BackgroundWorker> 事件与用户界面进行通信。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#5)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#5)]
     [!code-vb[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#5)]  
  
4.  在 `startAsyncButton` 控件的 <xref:System.Windows.Forms.Control.Click> 事件处理程序中，添加启动异步操作的代码。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#13](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#13)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#13](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#13)]
     [!code-vb[System.ComponentModel.BackgroundWorker#13](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#13)]  
  
5.  在 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件处理程序中，将计算结果分配给 `resultLabel` 控件。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#6](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#6)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#6)]
     [!code-vb[System.ComponentModel.BackgroundWorker#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#6)]  
  
## 添加进度报告和取消支持  
 由于异步操作将会花费很长的时间，因此通常希望向用户报告进度并允许用户取消操作。  <xref:System.ComponentModel.BackgroundWorker> 类提供一种在后台操作进行时允许发送进度消息的事件。  它还提供一种允许辅助代码检测到 <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> 调用并中断自身的标记。  
  
#### 实现进度报告  
  
1.  在**“属性”**窗口中，选择 `backgroundWorker1`。  将 <xref:System.ComponentModel.BackgroundWorker.WorkerReportsProgress%2A> 和 <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> 属性设置为 `true`。  
  
2.  在 `FibonacciCalculator` 窗体中声明两个变量。  这将用来跟踪进度。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#14](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#14)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#14](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#14)]
     [!code-vb[System.ComponentModel.BackgroundWorker#14](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#14)]  
  
3.  为 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件添加事件处理程序。  在 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件处理程序中，用 <xref:System.ComponentModel.ProgressChangedEventArgs> 参数的 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> 属性更新 <xref:System.Windows.Forms.ProgressBar>。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#7](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#7)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#7)]
     [!code-vb[System.ComponentModel.BackgroundWorker#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#7)]  
  
#### 实现取消支持  
  
1.  在 `cancelAsyncButton` 控件的 <xref:System.Windows.Forms.Control.Click> 事件处理程序中，添加取消异步操作的代码。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#4](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#4)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#4)]
     [!code-vb[System.ComponentModel.BackgroundWorker#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#4)]  
  
2.  下面的 `ComputeFibonacci` 方法中的代码片段可报告进程并支持取消。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#11](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#11)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#11)]
     [!code-vb[System.ComponentModel.BackgroundWorker#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#11)]  
    [!code-cpp[System.ComponentModel.BackgroundWorker#12](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#12)]
    [!code-csharp[System.ComponentModel.BackgroundWorker#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#12)]
    [!code-vb[System.ComponentModel.BackgroundWorker#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#12)]  
  
## 检查点  
 此时，您就可以编译并运行斐波那契数列计算器应用程序了。  
  
#### 测试项目  
  
-   按 F5 以编译并运行应用程序。  
  
     在后台运行计算的同时，将会看到 <xref:System.Windows.Forms.ProgressBar> 显示完成计算的进度。  也可以取消未完成的操作。  
  
     对于很小的数值，计算应非常快，但对于较大的数值，将看到明显的延时。  如果输入 30 或更大的值，应看到有几秒钟的延时，这取决于计算机的速度。  对于大于 40 的值，完成计算可能要花费数分钟或数小时。  在计算器计算很大的斐波那契数列时，注意可以自由地移动窗体、最小化、最大化甚至关闭它。  这是因为主 UI 线程并不等待计算完成。  
  
## 后续步骤  
 现在已经实现了一个利用 <xref:System.ComponentModel.BackgroundWorker> 组件来在后台执行计算的窗体，可以研究异步操作的其他可能性：  
  
-   在同时进行的几项操作中使用多个 <xref:System.ComponentModel.BackgroundWorker> 对象。  
  
-   要调试多线程应用程序，请参见 [如何：使用“线程”窗口](../Topic/How%20to:%20Use%20the%20Threads%20Window.md)。  
  
-   实现自己的支持异步编程模式的组件。  有关更多信息，请参见 [Event\-based Asynchronous Pattern Overview](../../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)。  
  
    > [!CAUTION]
    >  使用任何一种多线程都可能引起极为严重和复杂的 bug。  在实现任何使用多线程的解决方案之前，请参考 [Managed Threading Best Practices](../../../../docs/standard/threading/managed-threading-best-practices.md)。  
  
## 请参阅  
 <xref:System.ComponentModel.BackgroundWorker>   
 [Managed Threading Best Practices](../../../../docs/standard/threading/managed-threading-best-practices.md)   
 [组件中的多线程处理](../Topic/Multithreading%20in%20Components.md)   
 [NOT IN BUILD: Multithreading in Visual Basic](http://msdn.microsoft.com/zh-cn/c731a50c-09c1-4468-9646-54c86b75d269)   
 [如何：实现使用后台操作的窗体](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [演练：在后台运行操作](../../../../docs/framework/winforms/controls/walkthrough-running-an-operation-in-the-background.md)   
 [BackgroundWorker 组件](../../../../docs/framework/winforms/controls/backgroundworker-component.md)