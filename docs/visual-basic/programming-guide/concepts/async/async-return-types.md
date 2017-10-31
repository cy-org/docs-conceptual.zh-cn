---
title: "异步返回类型 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 07890291-ee72-42d3-932a-fa4d312f2c60
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 703d3fc3f503017edf38521d77f9b15a92d0ebf3
ms.lasthandoff: 03/13/2017

---
# <a name="async-return-types-visual-basic"></a>异步返回类型 (Visual Basic)
Async 方法具有三个可能的返回类型︰ <xref:System.Threading.Tasks.Task%601>， <xref:System.Threading.Tasks.Task>，和 void。</xref:System.Threading.Tasks.Task> </xref:System.Threading.Tasks.Task%601> 在 Visual Basic 中形式写入 void 返回类型[Sub](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)过程。 有关异步方法的详细信息，请参阅[使用 Async 和 Await (Visual Basic 中) 的异步编程](../../../../visual-basic/programming-guide/concepts/async/index.md)。  
  
 在以下其中一节检查每个返回类型，且在本主题末尾可以找到使用全部三种类型的完整示例。  
  
> [!NOTE]
>  若要运行该示例，必须具有 Visual Studio 2012 或更高版本和.NET Framework 4.5 或更高版本安装在您的计算机上。  
  
##  <a name="BKMK_TaskTReturnType"></a>Task （t） 返回类型  
 <xref:System.Threading.Tasks.Task%601>返回类型可用于异步方法，其中包含[返回](../../../../visual-basic/language-reference/statements/return-statement.md)语句，则该操作数类型`TResult`。</xref:System.Threading.Tasks.Task%601>  
  
 在下面的示例中，`TaskOfT_MethodAsync`异步方法包含的 return 语句，返回一个整数。 因此，该方法声明必须指定返回类型为`Task(Of Integer)`。  
  
```vb  
' TASK(OF T) EXAMPLE  
Async Function TaskOfT_MethodAsync() As Task(Of Integer)  
  
    ' The body of an async method is expected to contain an awaited   
    ' asynchronous call.  
    ' Task.FromResult is a placeholder for actual work that returns a string.  
    Dim today As String = Await Task.FromResult(Of String)(DateTime.Now.DayOfWeek.ToString())  
  
    ' The method then can process the result in some way.  
    Dim leisureHours As Integer  
    If today.First() = "S" Then  
        leisureHours = 16  
    Else  
        leisureHours = 5  
    End If  
  
    ' Because the return statement specifies an operand of type Integer, the   
    ' method must have a return type of Task(Of Integer).   
    Return leisureHours  
End Function  
```  
  
 当`TaskOfT_MethodAsync`称为从在 await 表达式中，await 表达式中检索的整数值 (值`leisureHours`) 存储在由返回的任务`TaskOfT_MethodAsync`。 有关详细信息 await 表达式，请参阅[Await 运算符](../../../../visual-basic/language-reference/operators/await-operator.md)。  
  
 下面的代码调用和等待方法`TaskOfT_MethodAsync`。 结果赋给`result1`变量。  
  
```vb  
' Call and await the Task(Of T)-returning async method in the same statement.  
Dim result1 As Integer = Await TaskOfT_MethodAsync()  
```  
  
 您可以更好地理解了这种分隔对调用`TaskOfT_MethodAsync`的应用程序从`Await`，如下面的代码所示。 对方法的调用`TaskOfT_MethodAsync`这并不是立即处于等待状态的返回`Task(Of Integer)`，正如您期望的声明中的方法。 该任务指派给`integerTask`变量在示例中。 因为`integerTask`是<xref:System.Threading.Tasks.Task%601>，它包含<xref:System.Threading.Tasks.Task%601.Result>类型的属性`TResult`。</xref:System.Threading.Tasks.Task%601.Result> </xref:System.Threading.Tasks.Task%601> 在这种情况下，TResult 表示整数类型。 当`Await`应用于`integerTask`，await 表达式的计算结果的内容为<xref:System.Threading.Tasks.Task%601.Result%2A>属性`integerTask`。</xref:System.Threading.Tasks.Task%601.Result%2A> 将值赋给`result2`变量。  
  
> [!WARNING]
>  <xref:System.Threading.Tasks.Task%601.Result%2A>属性是阻塞属性。</xref:System.Threading.Tasks.Task%601.Result%2A> 如果你在其任务完成之前尝试访问它，当前处于活动状态的线程将被阻止，直到任务完成且值为可用。 在大多数情况下，应通过使用访问值`Await`而不是直接访问的属性。  
  
```vb  
' Call and await in separate statements.  
Dim integerTask As Task(Of Integer) = TaskOfT_MethodAsync()  
  
' You can do other work that does not rely on resultTask before awaiting.  
textBox1.Text &= String.Format("Application can continue working while the Task(Of T) runs. . . . " & vbCrLf)  
  
Dim result2 As Integer = Await integerTask  
```  
  
 下面的代码中的显示语句验证的值`result1`变量，`result2`变量，与`Result`是相同的属性。 请记住，`Result`属性是阻塞属性，并且之前等待的 task 不应访问。  
  
```vb  
' Display the values of the result1 variable, the result2 variable, and  
' the resultTask.Result property.  
textBox1.Text &= String.Format(vbCrLf & "Value of result1 variable:   {0}" & vbCrLf, result1)  
textBox1.Text &= String.Format("Value of result2 variable:   {0}" & vbCrLf, result2)  
textBox1.Text &= String.Format("Value of resultTask.Result:  {0}" & vbCrLf, integerTask.Result)  
```  
  
##  <a name="BKMK_TaskReturnType"></a>任务返回类型  
 不包含 return 语句或包含通常不返回操作数的 return 语句的 Async 方法具有返回类型为<xref:System.Threading.Tasks.Task>。</xref:System.Threading.Tasks.Task> 这种方法应为[Sub](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)过程，如果它们编写的同步运行。 如果您使用`Task`返回类型对于异步方法中，调用的方法可以使用`Await`运算符可暂停调用方的完成直到完成调用的异步方法。  
  
 在下面的示例中，异步方法`Task_MethodAsync`不包含 return 语句。 因此，您指定的返回类型为`Task`对于方法，这样`Task_MethodAsync`以等待。 定义`Task`类型不包括`Result`属性存储返回值。  
  
```vb  
' TASK EXAMPLE  
Async Function Task_MethodAsync() As Task  
  
    ' The body of an async method is expected to contain an awaited   
    ' asynchronous call.  
    ' Task.Delay is a placeholder for actual work.  
    Await Task.Delay(2000)  
    textBox1.Text &= String.Format(vbCrLf & "Sorry for the delay. . . ." & vbCrLf)  
  
    ' This method has no return statement, so its return type is Task.   
End Function  
```  
  
 `Task_MethodAsync`调用该方法并使用 await 语句而不是 await 表达式，类似于同步的调用语句等待`Sub`或返回 void 的方法。 应用程序的`Await`运算符在这种情况下不生成值。  
  
 下面的代码调用和等待方法`Task_MethodAsync`。  
  
```vb  
' Call and await the Task-returning async method in the same statement.  
Await Task_MethodAsync()  
```  
  
 如下所示的上一个<xref:System.Threading.Tasks.Task%601>示例中，可以单独对调用`Task_MethodAsync`的应用程序从`Await`运算符，如以下代码所示。</xref:System.Threading.Tasks.Task%601> 但是，请记住，`Task`没有`Result`属性，并当 await 运算符应用于生成没有值`Task`。  
  
 下面的代码分隔调用`Task_MethodAsync`从等待该任务，`Task_MethodAsync`返回。  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
##  <a name="BKMK_VoidReturnType"></a>Void 返回类型  
 主要用途`Sub`过程是在事件处理程序，其中没有返回类型 （也称为 void 返回类型用其他语言）。 Void 返回还可用于替代返回 void 的方法，或者用于执行可分类为"发后不理"活动的方法。 但是，您应返回`Task`只要有可能，因为不能等待返回 void 的异步方法。 这种方法的任何调用方必须能够继续完成，而无需等待调用的异步方法完成，并且调用方必须独立于异步方法生成的任何值或异常。  
  
 返回 void 的异步方法的调用方无法捕获从该方法引发的异常，且此类未经处理的异常可能会导致应用程序故障。 如果返回的异步方法中发生异常<xref:System.Threading.Tasks.Task>或<xref:System.Threading.Tasks.Task%601>，存储在返回的任务，并等待该任务时再次引发异常。</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task> 因此，请确保可以产生异常任何 async 方法都具有返回类型为<xref:System.Threading.Tasks.Task>或<xref:System.Threading.Tasks.Task%601>和对方法的调用会等待。</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task>  
  
 有关如何在异步方法中捕捉异常的详细信息，请参阅[重试...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
 下面的代码定义了异步事件处理程序。  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
##  <a name="BKMK_Example"></a>完整的示例  
 以下 Windows Presentation Foundation (WPF) 项目包含本主题中的代码示例。  
  
 若要运行项目，请执行下列步骤：  
  
1.  启动 Visual Studio。  
  
2.  在菜单栏上，依次选择“文件” ****、“新建” ****、“项目” ****。  
  
     **“新建项目”** 对话框随即打开。  
  
3.  在**已安装**，**模板**类别中，选择**Visual Basic**，然后选择**Windows**。 选择**WPF 应用程序**从项目类型列表。  
  
4.  输入`AsyncReturnTypes`作为项目的名称，然后选择**确定**按钮。  
  
     新项目将出现在**解决方案资源管理器**。  
  
5.  在 Visual Studio 代码编辑器中，选择 **“MainWindow.xaml”** 选项卡。  
  
     如果选项卡不可见，打开快捷菜单中的 MainWindow.xaml**解决方案资源管理器**，然后选择**打开**。  
  
6.  在**XAML** MainWindow.xaml，窗口将替换为下面的代码的代码。  
  
    ```vb  
    <Window x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="button1" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="button1_Click"/>  
            <TextBox x:Name="textBox1" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
  
        </Grid>  
    </Window>  
  
    ```  
  
     一个简单的窗口，其中包含一个文本框和一个按钮将出现在**设计**MainWindow.xaml 的窗口。  
  
7.  在**解决方案资源管理器**，MainWindow.xaml.vb，打开快捷菜单，然后选择**查看代码**。  
  
8.  将 MainWindow.xaml.vb 中的代码替换为以下代码。  
  
    ```vb  
    Class MainWindow  
  
        ' SUB EXAMPLE  
        Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click  
  
            textBox1.Clear()  
  
            ' Start the process and await its completion. DriverAsync is a   
            ' Task-returning async method.  
            Await DriverAsync()  
  
            ' Say goodbye.  
            textBox1.Text &= vbCrLf & "All done, exiting button-click event handler."  
        End Sub  
  
        Async Function DriverAsync() As Task  
  
            ' Task(Of T)   
            ' Call and await the Task(Of T)-returning async method in the same statement.  
            Dim result1 As Integer = Await TaskOfT_MethodAsync()  
  
            ' Call and await in separate statements.  
            Dim integerTask As Task(Of Integer) = TaskOfT_MethodAsync()  
  
            ' You can do other work that does not rely on resultTask before awaiting.  
            textBox1.Text &= String.Format("Application can continue working while the Task(Of T) runs. . . . " & vbCrLf)  
  
            Dim result2 As Integer = Await integerTask  
  
            ' Display the values of the result1 variable, the result2 variable, and  
            ' the resultTask.Result property.  
            textBox1.Text &= String.Format(vbCrLf & "Value of result1 variable:   {0}" & vbCrLf, result1)  
            textBox1.Text &= String.Format("Value of result2 variable:   {0}" & vbCrLf, result2)  
            textBox1.Text &= String.Format("Value of resultTask.Result:  {0}" & vbCrLf, integerTask.Result)  
  
            ' Task   
            ' Call and await the Task-returning async method in the same statement.  
            Await Task_MethodAsync()  
  
            ' Call and await in separate statements.  
            Dim simpleTask As Task = Task_MethodAsync()  
  
            ' You can do other work that does not rely on simpleTask before awaiting.  
            textBox1.Text &= String.Format(vbCrLf & "Application can continue working while the Task runs. . . ." & vbCrLf)  
  
            Await simpleTask  
        End Function  
  
        ' TASK(OF T) EXAMPLE  
        Async Function TaskOfT_MethodAsync() As Task(Of Integer)  
  
            ' The body of an async method is expected to contain an awaited   
            ' asynchronous call.  
            ' Task.FromResult is a placeholder for actual work that returns a string.  
            Dim today As String = Await Task.FromResult(Of String)(DateTime.Now.DayOfWeek.ToString())  
  
            ' The method then can process the result in some way.  
            Dim leisureHours As Integer  
            If today.First() = "S" Then  
                leisureHours = 16  
            Else  
                leisureHours = 5  
            End If  
  
            ' Because the return statement specifies an operand of type Integer, the   
            ' method must have a return type of Task(Of Integer).   
            Return leisureHours  
        End Function  
  
        ' TASK EXAMPLE  
        Async Function Task_MethodAsync() As Task  
  
            ' The body of an async method is expected to contain an awaited   
            ' asynchronous call.  
            ' Task.Delay is a placeholder for actual work.  
            Await Task.Delay(2000)  
            textBox1.Text &= String.Format(vbCrLf & "Sorry for the delay. . . ." & vbCrLf)  
  
            ' This method has no return statement, so its return type is Task.   
        End Function  
  
    End Class  
    ```  
  
9. 按 F5 键以运行程序，然后选择 **“启动”** 按钮。  
  
     应出现以下输出。  
  
    ```  
    Application can continue working while the Task<T> runs. . . .   
  
    Value of result1 variable:   5  
    Value of result2 variable:   5  
    Value of integerTask.Result: 5  
  
    Sorry for the delay. . . .  
  
    Application can continue working while the Task runs. . . .  
  
    Sorry for the delay. . . .  
  
    All done, exiting button-click event handler.  
    ```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.Tasks.Task.FromResult%2A></xref:System.Threading.Tasks.Task.FromResult%2A>   
 [演练︰ 访问 Web 使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [异步程序 (Visual Basic 中) 中的控制流](../../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)   
 [异步](../../../../visual-basic/language-reference/modifiers/async.md)   
 [Await 运算符](../../../../visual-basic/language-reference/operators/await-operator.md)
