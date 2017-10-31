---
title: "Walkthrough: Implementing a Component That Supports the Event-based Asynchronous Pattern | Microsoft Docs"
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
ms.assetid: 61f676b5-936f-40f6-83ce-f22805ec9c2f
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Walkthrough: Implementing a Component That Supports the Event-based Asynchronous Pattern
如果您正在编写一个类，其中某些操作可能导致显著延迟，请考虑通过实现 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md) 赋予此类异步功能。  
  
 此演练介绍如何创建可实现基于事件的异步模式的组件。  它是通过使用 <xref:System.ComponentModel?displayProperty=fullName> 命名空间的帮助器类实现的，这确保了此组件可以在任何应用程序模型（包括 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]、控制台应用程序和 Windows 窗体应用程序）下正常运行。  您还可以用 <xref:System.Windows.Forms.PropertyGrid> 控件和您自己的自定义设计器设计此组件。  
  
 完成后，您将拥有一个可异步计算质数的应用程序。  您的应用程序将有一个主用户界面 \(UI\) 线程和一个用于各个质数计算的线程。  虽然测试一个较大的数字是否是质数可能需要很长的时间，但是主 UI 线程不会被此延迟中断，并且该窗体在计算期间具有响应能力。  您将能够并行运行任意数量的计算，并能够有选择地取消挂起的计算。  
  
 本演练涉及以下任务：  
  
-   创建组件  
  
-   定义公共异步事件和委托  
  
-   定义私有委托  
  
-   实现公共事件  
  
-   实现完成方法  
  
-   实现辅助方法  
  
-   实现启动和取消方法  
  
 若要将本主题中的代码复制为单个列表，请参见[How to: Implement a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)。  
  
## 创建组件  
 第一步是创建将实现基于事件的异步模式的组件。  
  
#### 创建组件  
  
-   创建一个名为 `PrimeNumberCalculator`、从 <xref:System.ComponentModel.Component> 继承的类。  
  
## 定义公共异步事件和委托  
 您的组件使用事件与客户端通信。  异步任务完成后，*方法名称MethodName*`Completed 事件会向客户端发出警报，方法名称` `ProgressChanged` 事件还会通知客户端异步任务的进度。  
  
#### 为您的组件的客户端定义异步事件：  
  
1.  在您的文件的顶部导入 <xref:System.Threading?displayProperty=fullName> 和 <xref:System.Collections.Specialized?displayProperty=fullName> 命名空间。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#11](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#11)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#11](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#11)]  
  
2.  在  `PrimeNumberCalculator`  类定义之前，声明进度和完成事件的委托。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#7](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#7)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#7](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#7)]  
  
3.  在  `PrimeNumberCalculator`  类定义中，向客户端声明报告进度事件和完成事件。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#8](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#8)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#8](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#8)]  
  
4.  在  `PrimeNumberCalculator`  类定义之后，派生  `CalculatePrimeCompletedEventArgs`  类，用于向客户端的 `CalculatePrimeCompleted` 事件的事件处理程序报告各个计算的结果。  除了 `AsyncCompletedEventArgs` 属性，此类还能使客户端确定测试的是什么数，是不是质数，如果不是质数，它的第一个约数是什么。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#6](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#6)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#6](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#6)]  
  
## 检查点  
 此时，您就可以生成组件了。  
  
#### 测试组件  
  
-   编译组件。  
  
     您将会接收到两个编译器警告：  
  
    ```  
    warning CS0067: The event 'AsynchronousPatternExample.PrimeNumberCalculator.ProgressChanged' is never used  
    warning CS0067: The event 'AsynchronousPatternExample.PrimeNumberCalculator.CalculatePrimeCompleted' is never used  
    ```  
  
     这些警告将在下一部分中清除。  
  
## 定义私有委托  
 `PrimeNumberCalculator`  组件的异步方面是通过在内部使用称为 <xref:System.Threading.SendOrPostCallback> 的特殊委托实现的。  <xref:System.Threading.SendOrPostCallback> 表示在 <xref:System.Threading.ThreadPool> 线程上执行的回调方法。  回调方法必须有一个采用 <xref:System.Object> 类型的一个参数的签名，这意味着您将需要在包装类中的委托之间传递状态。  有关详细信息，请参阅<xref:System.Threading.SendOrPostCallback>。  
  
#### 实现组件的内部异步行为：  
  
1.  在  `PrimeNumberCalculator`  类中声明和创建 <xref:System.Threading.SendOrPostCallback> 委托。  在名为  `InitializeDelegates` 的实用工具方法中创建 <xref:System.Threading.SendOrPostCallback> 对象。  
  
     您将需要两个委托：一个用于向客户端报告进程，一个用于向客户端报告完成。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#9](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#9)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#9](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#9)]  
    [!code-csharp[System.ComponentModel.AsyncOperationManager#20](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#20)]
    [!code-vb[System.ComponentModel.AsyncOperationManager#20](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#20)]  
  
2.  在组件的构造函数中调用 `InitializeDelegates` 方法。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#21](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#21)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#21](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#21)]  
  
3.  声明 `PrimeNumberCalculator` 类中的一个委托，该类用于处理要异步完成的实际工作。  此委托将包装用于测试一个数是否是质数的辅助方法。  此委托采用 <xref:System.ComponentModel.AsyncOperation> 参数，用于跟踪异步操作的生存期。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#22](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#22)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#22](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#22)]  
  
4.  创建一个集合，用来管理挂起的异步操作的生存期。  客户端需要一种方式来跟踪操作的执行和完成情况，此跟踪的实现需要客户端在调用异步方法时传递一个唯一标记或任务 ID。  `PrimeNumberCalculator` 组件必须通过将任务 ID 与其对应的调用关联起来以跟踪每个调用。  如果客户端传递的任务 ID 不是唯一的，则 `PrimeNumberCalculator` 组件必须引发一个异常。  
  
     `PrimeNumberCalculator` 组件通过使用名为 <xref:System.Collections.Specialized.HybridDictionary> 的特殊集合类来跟踪任务 ID。  在类定义中，创建一个名为  `userTokenToLifetime` 的 <xref:System.Collections.Specialized.HybridDictionary>。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#23](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#23)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#23](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#23)]  
  
## 实现公共事件  
 那些实现基于事件的异步模式的组件会使用事件来与客户端进行通信。  借助 <xref:System.ComponentModel.AsyncOperation> 类，可以在适当的线程上调用这些事件。  
  
#### 向组件的客户端引发事件：  
  
1.  实现用于向客户端报告的公共事件。  您将需要一个用于报告进度的事件和一个用于报告完成的事件。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#24](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#24)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#24](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#24)]  
  
## 实现完成方法  
 完成委托是一个方法，在异步操作因成功完成、出现错误或发生取消而结束时，基础的自由线程异步行为会调用此方法。  此调用可在任意线程上发生。  
  
 从唯一客户端标记的内部集合中移除客户端任务 ID 就需要使用此方法。  此方法还可以通过在相应的 <xref:System.ComponentModel.AsyncOperation> 上调用 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> 方法来结束某个特定异步操作的生存期。  此调用将在适合于应用程序模型的线程上引发完成事件。  调用 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> 方法后，<xref:System.ComponentModel.AsyncOperation> 的这一实例不再可用。此后，任何尝试使用此实例的行为都将引发异常。  
  
 `CompletionMethod` 签名必须包含描述异步操作的结果所必需的所有状态。  它包含此特定异步操作所测试的数字的状态，此数是不是质数，如果不是质数，那么它的第一个约数是什么。  它还包含描述任何发生的异常和对应于此特定任务的 <xref:System.ComponentModel.AsyncOperation> 的状态。  
  
#### 完成异步操作：  
  
-   实现完成方法。  它采用六个参数；在通过客户端的  `CalculatePrimeCompletedEventHandler` 返回客户端的  `CalculatePrimeCompletedEventArgs` 中填充的就是这些参数。  它将客户端的任务 ID 标记从内部集合中移除，然后调用 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> 结束异步操作的生存期。  <xref:System.ComponentModel.AsyncOperation> 会将此调用封送到适合于应用程序模型的线程或上下文。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#26](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#26)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#26](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#26)]  
  
## 检查点  
 此时，您就可以生成组件了。  
  
#### 测试组件  
  
-   编译组件。  
  
     您将接收到一个编译器警告：  
  
    ```  
    warning CS0169: The private field 'AsynchronousPatternExample.PrimeNumberCalculator.workerDelegate' is never used  
    ```  
  
     此警告将在下一部分中解决。  
  
## 实现辅助方法  
 到目前为止，您已为 `PrimeNumberCalculator` 组件实现了支持的异步代码。  现在，您可以实现执行实际工作的代码。  您将实现三种方法：`CalculateWorker`, `BuildPrimeNumberList` 和 `IsPrime`。  `BuildPrimeNumberList` 和 `IsPrime` 共同构成众所周知的称为埃拉托色尼过滤 \(Sieve of Eratosthenes\) 的算法，此算法通过查找测试数的平方根之内的所有质数来确定一个数是不是质数。  如果没有发现任何约数，则测试数是质数。  
  
 如果编写的这个组件要实现最高效率，则它应记住对不同测试数的各种调用所发现的所有质数。  它还会检查最小约数，如 2、3 和 5。  此示例是为了演示如何异步执行耗时的操作，不过，这些优化操作将作为练习留给您来做。  
  
 `CalculateWorker` 方法包装在一个委托中，可通过调用 `BeginInvoke` 来异步调用此方法。  
  
> [!NOTE]
>  进程报告在 `BuildPrimeNumberList` 方法中实现。  在运行速度快的计算机上，可快速连续引发 `ProgressChanged` 事件。  引发这些事件的客户端线程必须能够处理这种情形。  用户界面代码可能会被大量的消息所淹没，无法继续，结果导致挂起行为。  有关处理此情形的示例用户界面，请参见[How to: Implement a Client of the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)。  
  
#### 异步执行质数计算：  
  
1.  实现 `TaskCanceled` 实用工具方法。  它会检查任务生存期集合中是否存在给定任务 ID，如果没有找到该任务 ID，则返回 `true`。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#32](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#32)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#32](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#32)]  
  
2.  实现 `CalculateWorker` 方法。  它采用两个参数：一个是要测试的数，一个是 <xref:System.ComponentModel.AsyncOperation>。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#27](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#27)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#27](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#27)]  
  
3.  实现 `BuildPrimeNumberList`。  它采用两个参数：要测试的数和 <xref:System.ComponentModel.AsyncOperation>。  它使用 <xref:System.ComponentModel.AsyncOperation> 来报告进度和增量结果。  这确保了在应用程序模型的适当线程或上下文上调用客户端的事件处理程序。  如果 `BuildPrimeNumberList` 找到了一个质数，它会将该数作为增量结果报告给 `ProgressChanged` 事件的客户端事件处理程序。  此时，就需要一个自 <xref:System.ComponentModel.ProgressChangedEventArgs> 派生的名为 `CalculatePrimeProgressChangedEventArgs` 类；该类有一个新增的属性，名为 `LatestPrimeNumber`。  
  
     `BuildPrimeNumberList` 方法还会定期调用 `TaskCanceled` 方法，当该方法返回 `true` 时它就会退出。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#5)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#5)]  
  
4.  实现 `IsPrime`。  它采用三个参数：已知质数列表、要测试的数和找到的第一个约数的输出参数。  根据质数列表，它确定测试数是不是质数。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#28](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#28)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#28](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#28)]  
  
5.  自 <xref:System.ComponentModel.ProgressChangedEventArgs> 派生 `CalculatePrimeProgressChangedEventArgs`。  此类是将增量结果报告给客户端的 `ProgressChanged` 事件的事件处理程序所必需的。  它有一个新增的属性，名为 `LatestPrimeNumber`。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#29](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#29)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#29](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#29)]  
  
## 检查点  
 此时，您就可以生成组件了。  
  
#### 测试组件  
  
-   编译组件。  
  
     只剩下编写启动和取消异步操作的方法、`CalculatePrimeAsync` 和 `CancelAsync`。  
  
## 实现启动和取消方法  
 通过在包装辅助方法的委托上调用 `BeginInvoke` 可在其自己的线程上启动该辅助方法。  若要管理特定异步操作的生存期，请调用 <xref:System.ComponentModel.AsyncOperationManager> 帮助器类上的 <xref:System.ComponentModel.AsyncOperationManager.CreateOperation%2A> 方法。  这将返回 <xref:System.ComponentModel.AsyncOperation>，它会将对客户端事件处理程序的调用封送到合适的线程或上下文。  
  
 通过在特定挂起的操作对应的 <xref:System.ComponentModel.AsyncOperation> 上调用 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> 可以取消此操作。  这就结束了此操作，对其 <xref:System.ComponentModel.AsyncOperation> 的任何后续调用都会引发异常。  
  
#### 实现启动和取消功能：  
  
1.  实现 `CalculatePrimeAsync` 方法。  确保客户端提供的标记（任务 ID）相对于表示当前挂起的任务的所有标记是唯一的。  如果客户端传入的标记不是唯一的，则 `CalculatePrimeAsync` 会引发异常。  否则，将此标记添加到任务 ID 集合中。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#3)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#3)]  
  
2.  实现 `CancelAsync` 方法。  如果标记集合中存在 `taskId` 参数，则会将其移除。  这会阻止未启动的已取消任务运行。  如果该任务正在运行，则当 `BuildPrimeNumberList` 方法检测出已从生存期集合中移除了任务 ID 时，该方法将退出。  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#4)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#4)]  
  
## 检查点  
 此时，您就可以生成组件了。  
  
#### 测试组件  
  
-   编译组件。  
  
 `PrimeNumberCalculator`  组件现在已完成，您可以随时使用它了。  
  
 有关使用 `PrimeNumberCalculator` 组件的示例客户端，请参见[How to: Implement a Client of the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)。  
  
## 后续步骤  
 您可以通过编写 `CalculatePrime`（`CalculatePrimeAsync` 方法的同步等效方法）来填写此示例。  这会使 `PrimeNumberCalculator` 组件完全符合基于事件的异步模式。  
  
 您可以通过保留由不同测试数的各种调用所发现的所有质数的列表来改进此示例。  使用此方法，每个任务都会从前面的任务所做的工作中受益。  使用 `lock` 区域保护此列表时要小心，这样会序列化不同线程对此列表的访问。  
  
 您也可以通过测试最小约数（如 2、3 和 5）来改进此示例。  
  
## 请参阅  
 [如何：在后台运行操作](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)   
 [NOT IN BUILD: Multithreading in Visual Basic](http://msdn.microsoft.com/zh-cn/c731a50c-09c1-4468-9646-54c86b75d269)   
 [How to: Implement a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)   
 [Multithreaded Programming with the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)