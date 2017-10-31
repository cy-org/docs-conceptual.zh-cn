---
title: "实现基于事件的异步模式 | Microsoft Docs"
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
  - "基于事件的异步模式"
  - "ProgressChangedEventArgs 类"
  - "BackgroundWorker 组件"
  - "事件 [.NET Framework], 异步"
  - "异步模式"
  - "AsyncOperationManager 类"
  - "线程处理 [.NET Framework], 异步功能"
  - "组件 [.NET Framework] 异步"
  - "AsyncOperation 类"
  - "AsyncCompletedEventArgs 类"
ms.assetid: 43402d19-8d30-426d-8785-1a4478233bfa
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 实现基于事件的异步模式
如果您正在编写具有某些操作可能会带来明显的延迟的类，请考虑通过实现提供异步功能[基于事件的异步模式概述](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)。  
  
 基于事件的异步模式提供了标准化的方式打包具有异步功能的类。 如果使用的帮助器类实现如下所示<xref:System.ComponentModel.AsyncOperationManager>，您的类将正常工作在任何应用程序模型，包括[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]，控制台应用程序和 Windows 窗体应用程序。  
  
 实现基于事件的异步模式示例，请参阅[如何︰ 实现支持基于事件的异步模式的组件](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)。  
  
 对于简单的异步操作，您可能会发现<xref:System.ComponentModel.BackgroundWorker>合适的组件。 有关详细信息<xref:System.ComponentModel.BackgroundWorker>，请参阅[如何︰ 在后台运行操作](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)。  
  
 以下列表介绍本主题中讨论的基于事件的异步模式的功能。  
  
-   为实现基于事件的异步模式的机会  
  
-   指定异步方法  
  
-   可以选择支持取消  
  
-   选择性地分别支持 IsBusy 属性  
  
-   （可选） 为进度报告提供支持  
  
-   可以选择对返回增量结果提供支持  
  
-   处理 Out 和 Ref 参数在方法中  
  
## <a name="opportunities-for-implementing-the-event-based-asynchronous-pattern"></a>为实现基于事件的异步模式的机会  
 请考虑实现基于事件的异步模式时︰  
  
-   类的客户端不需要<xref:System.Threading.WaitHandle>和<xref:System.IAsyncResult>对象可用于异步操作，意味着轮询和<xref:System.Threading.WaitHandle.WaitAll%2A>或<xref:System.Threading.WaitHandle.WaitAny%2A>需要构建由客户端。  
  
-   您希望能够通过熟悉的事件/委托模型为客户端管理的异步操作。  
  
 任何操作的异步实现的候选项，但是应考虑那些希望会产生较长的延迟。 尤其是合适的操作的客户端调用方法，并向您发送通知完成时，无需进一步的干预。 也是合适的连续运行、 定期通知进度、 增量结果和状态更改的客户端的操作。  
  
 决定何时支持基于事件的异步模式的详细信息，请参阅[决定何时实现基于事件的异步模式](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)。  
  
## <a name="naming-asynchronous-methods"></a>指定异步方法  
 对于每个同步方法*MethodName*要为其提供了异步对应项︰  
  
 定义*MethodName* `Async`方法的︰  
  
-   返回 `void`。  
  
-   采用相同参数作为*MethodName*方法。  
  
-   接受多个调用。  
  
 还可以定义*MethodName* `Async`重载时，等于*MethodName*`Async`，但具有附加的对象值的参数调用`userState`。 如果已准备好开始管理多个并发调用的方法中，在这种情况下执行此操作`userState`值将传递回所有事件处理程序来区分在方法的调用。 您还可以选择这样做只是作为一个位置来存储用户状态，以便于以后检索。  
  
 对于每个单独*MethodName* `Async`方法签名︰  
  
1.  在该方法相同的类中定义了以下事件︰  
  
    ```vb  
    Public Event MethodNameCompleted As MethodNameCompletedEventHandler  
    ```  
  
    ```csharp  
    public event MethodNameCompletedEventHandler MethodNameCompleted;  
    ```  
  
2.  定义以下委托和<xref:System.ComponentModel.AsyncCompletedEventArgs>。 这些值可能会超出类本身，但同一命名空间中定义。  
  
    ```vb  
    Public Delegate Sub MethodNameCompletedEventHandler( _  
        ByVal sender As Object, _  
        ByVal e As MethodNameCompletedEventArgs)  
  
    Public Class MethodNameCompletedEventArgs  
        Inherits System.ComponentModel.AsyncCompletedEventArgs  
    Public ReadOnly Property Result() As MyReturnType  
    End Property  
    ```  
  
    ```csharp  
    public delegate void MethodNameCompletedEventHandler(object sender,   
        MethodNameCompletedEventArgs e);  
  
    public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs  
    {  
        public MyReturnType Result { get; }  
    }  
    ```  
  
    -   确保*MethodName* `CompletedEventArgs`类将其成员公开为只读属性，而不是字段，因为字段会阻止数据绑定。  
  
    -   未定义任何<xref:System.ComponentModel.AsyncCompletedEventArgs>的派生类不会产生结果的方法。 只需使用的一个实例<xref:System.ComponentModel.AsyncCompletedEventArgs>本身。  
  
        > [!NOTE]
        >  在可行且适当，从而重新使用委托时，它是完全可以接受，和<xref:System.ComponentModel.AsyncCompletedEventArgs>类型。 在这种情况下，命名将不一致和方法名，因为给定的委托和<xref:System.ComponentModel.AsyncCompletedEventArgs>不会与单独某个方法。  
  
## <a name="optionally-support-cancellation"></a>可以选择支持取消  
 如果您的类将支持取消异步操作，则按如下所述，向客户端应公开取消。 请注意，有两个需取消支持在定义之前做出的决策点︰  
  
-   您的类，包括将来预计的添加到其中，有只需要一个支持取消操作的异步操作呢？  
  
-   是否可以支持多个挂起操作的取消支持的异步操作？ 也就是说，未*MethodName* `Async`方法是否采用`userState`参数，以及它是否允许多个调用在等待任何操作完成之前？  
  
 下表中使用这两个问题的答案确定取消方法的签名应该是什么。  
  
### <a name="visual-basic"></a>Visual Basic  
  
||支持的多个并行操作|一次只有一个操作|  
|------|------------------------------------------------|----------------------------------|  
|在整个类中的一个异步操作|`Sub MethodNameAsyncCancel(ByVal userState As Object)`|`Sub MethodNameAsyncCancel()`|  
|在类中的多个异步操作|`Sub CancelAsync(ByVal userState As Object)`|`Sub CancelAsync()`|  
  
### <a name="c"></a>C#  
  
||支持的多个并行操作|一次只有一个操作|  
|------|------------------------------------------------|----------------------------------|  
|在整个类中的一个异步操作|`void MethodNameAsyncCancel(object userState);`|`void MethodNameAsyncCancel();`|  
|在类中的多个异步操作|`void CancelAsync(object userState);`|`void CancelAsync();`|  
  
 如果您定义`CancelAsync(object userState)`方法中，客户端必须仔细选择它们以使其能够区分该对象上调用的所有异步方法的状态值时并不只是一个异步方法的所有调用之间。  
  
 命名单个异步操作版本决定*MethodName* `AsyncCancel`基于能够更轻松地发现类似 Visual Studio IntelliSense 的设计环境中的方法。 这组相关的成员，并将它们与具有与异步功能无关的其他成员区分开来。 如果需要，你可能需要其他异步操作添加在后续版本中，则最好定义`CancelAsync`。  
  
 同一个类中未定义从上表中的多个方法。 程序将毫无意义，或者它将变得混乱增生方法的类接口。  
  
 这些方法通常会立即返回，并可能会或可能无法实际取消该操作。 事件处理程序中*MethodName* `Completed`事件， *MethodName* `CompletedEventArgs`对象包含`Cancelled`字段中，客户端可以用来确定是否取消了操作。  
  
 遵守中所述的取消语义[实现基于事件的异步模式的最佳做法](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)。  
  
## <a name="optionally-support-the-isbusy-property"></a>选择性地分别支持 IsBusy 属性  
 如果您的类不支持多个并发调用，请考虑公开`IsBusy`属性。 这允许开发人员确定是否*MethodName* `Async`方法是否正在运行，而无需捕获的异常从*MethodName* `Async`方法。  
  
 遵守`IsBusy`中所述的语义[实现基于事件的异步模式的最佳做法](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)。  
  
## <a name="optionally-provide-support-for-progress-reporting"></a>（可选） 为进度报告提供支持  
 它是经常希望在其操作期间用于报告进度的异步操作。 基于事件的异步模式提供了有关执行此操作的准则。  
  
-   还可以定义一个事件，它由异步操作引发并在相应线程上调用。 <xref:System.ComponentModel.ProgressChangedEventArgs>对象携带应为介于 0 和 100 之间的整数值的进度指示器。  
  
-   此事件的名称，如下所示︰  
  
    -   `ProgressChanged`如果类具有多个异步操作 （或预期增长，以在将来版本中包括多个异步操作）;  
  
    -   *MethodName* `ProgressChanged`如果类具有一个异步操作。  
  
     此命名选择类似对取消方法中，进行可以选择支持取消部分中所述。  
  
 此事件应使用<xref:System.ComponentModel.ProgressChangedEventHandler>委托签名和<xref:System.ComponentModel.ProgressChangedEventArgs>类。 或者，如果可以 （对于实例、 读取的字节和下载操作的总字节数） 提供更多特定于域的进度指示器，则您应定义的派生的类<xref:System.ComponentModel.ProgressChangedEventArgs>。  
  
 请注意，只有一个`ProgressChanged`或*MethodName* `ProgressChanged`事件的类，而不管它支持的异步方法的数目。 客户端应使用`userState`对象传递给*MethodName* `Async`方法来区分上多个并发操作的进度更新。  
  
 可以在其中多个操作支持进度，且每个返回一个不同的进度指示器的情况。 在这种情况下，单个`ProgressChanged`事件不适当情况下，因此您可能要考虑支持多个`ProgressChanged`的事件。 在这种情况下使用的命名模式*MethodName* `ProgressChanged`为每个*MethodName* `Async`方法。  
  
 遵守所述的进度报告语义[实现基于事件的异步模式的最佳做法](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)。  
  
## <a name="optionally-provide-support-for-returning-incremental-results"></a>可以选择对返回增量结果提供支持  
 有时一个异步操作可以返回之前完成的增量结果。 有大量可用来支持此方案的选项。 下面是一些示例。  
  
### <a name="single-operation-class"></a>单操作类  
 如果您的类仅支持单个异步操作，并且能够返回增量结果，则该操作︰  
  
-   扩展<xref:System.ComponentModel.ProgressChangedEventArgs>类型以承载增量结果数据，并定义*MethodName* `ProgressChanged`使用此扩展数据的事件。  
  
-   引发此*MethodName* `ProgressChanged`事件报告的增量结果时。  
  
 此解决方案特别适用于单异步操作类因为存在与同一事件发生在"所有操作"上的增量结果返回为任何问题*MethodName* `ProgressChanged`事件的作用。  
  
### <a name="multiple-operation-class-with-homogeneous-incremental-results"></a>使用同构的增量结果的多个操作类  
 在这种情况下，您的类支持多个异步方法，每个能够返回增量结果和这些增量结果都具有相同类型的数据。  
  
 请按照上面描述的单一操作类，因为同一模型<xref:System.EventArgs>结构将用于所有的增量结果。 定义`ProgressChanged`而不是事件*MethodName* `ProgressChanged`事件，因为它适用于多个异步方法。  
  
### <a name="multiple-operation-class-with-heterogeneous-incremental-results"></a>使用异类增量结果的多个操作类  
 如果您的类支持多个异步方法，每个返回不同类型的数据，您应该︰  
  
-   分隔您增量结果报告与您的进度报告。  
  
-   定义单独的*MethodName* `ProgressChanged`具有合适的事件<xref:System.EventArgs>为每个异步方法来处理该方法的增量结果数据。  
  
 调用适当的线程上该事件处理程序中所述[实现基于事件的异步模式的最佳做法](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)。  
  
## <a name="handling-out-and-ref-parameters-in-methods"></a>处理 Out 和 Ref 参数在方法中  
 尽管使用`out`和`ref`，一般情况下，建议你不要在.NET Framework，以下是在存在时要遵循的规则︰  
  
 给定同步方法*MethodName*:  
  
-   `out`参数为*MethodName*不应属于*MethodName*`Async`。 相反，它们应属于*MethodName* `CompletedEventArgs`与中的等效参数同名*MethodName* （除非有更合适的名称）。  
  
-   `ref`参数为*MethodName*应显示为属于*MethodName*`Async`，以及作为的一部分*MethodName* `CompletedEventArgs`与中的等效参数同名*MethodName* （除非有更合适的名称）。  
  
 例如，给定︰  
  
```vb  
Public Function MethodName(ByVal arg1 As String, ByRef arg2 As String, ByRef arg3 As String) As Integer  
```  
  
```csharp  
public int MethodName(string arg1, ref string arg2, out string arg3);  
```  
  
 异步方法并将其<xref:System.ComponentModel.AsyncCompletedEventArgs>类将如下所示︰  
  
```vb  
Public Sub MethodNameAsync(ByVal arg1 As String, ByVal arg2 As String)  
  
Public Class MethodNameCompletedEventArgs  
    Inherits System.ComponentModel.AsyncCompletedEventArgs  
    Public ReadOnly Property Result() As Integer   
    End Property  
    Public ReadOnly Property Arg2() As String   
    End Property  
    Public ReadOnly Property Arg3() As String   
    End Property  
End Class  
```  
  
```csharp  
public void MethodNameAsync(string arg1, string arg2);  
  
public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs  
{  
    public int Result { get; };  
    public string Arg2 { get; };  
    public string Arg3 { get; };  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ComponentModel.ProgressChangedEventArgs>   
 <xref:System.ComponentModel.AsyncCompletedEventArgs>   
 [如何︰ 实现支持基于事件的异步模式的组件](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)   
 [如何︰ 在后台运行操作](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [如何︰ 实现使用后台操作的窗体](../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [确定何时实现基于事件的异步模式](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)   
 [使用基于事件的异步模式的多线程的编程](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)   
 [实现基于事件的异步模式的最佳做法](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)