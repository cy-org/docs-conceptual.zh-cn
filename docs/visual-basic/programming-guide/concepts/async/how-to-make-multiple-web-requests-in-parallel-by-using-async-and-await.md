---
title: "如何︰ 并行发起多个 Web 请求，使用 Async 和 Await (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: a894b99b-7cfd-4a38-adfb-20d24f986730
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e4c41cc3813a9f96d944d115c6aaa5c5842a629b
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await-visual-basic"></a>如何︰ 并行发起多个 Web 请求，使用 Async 和 Await (Visual Basic)
在异步方法中，它们创建时启动任务。 [Await](../../../../visual-basic/language-reference/operators/await-operator.md)运算符应用于该任务在任务完成之前无法继续处理的方法中的时刻。 通常一个任务被等待只要它创建的如以下示例所示。  
  
```vb  
Dim result = Await someWebAccessMethodAsync(url)  
```  
  
 但是，您可以分隔创建不依赖于任务的完成从正在等待该任务，如果您的程序具有其他工作来完成任务。  
  
```vb  
' The following line creates and starts the task.  
Dim myTask = someWebAccessMethodAsync(url)  
  
' While the task is running, you can do other work that does not depend  
' on the results of the task.  
' . . . . .  
  
' The application of Await suspends the rest of this method until the task is   
' complete.  
Dim result = Await myTask  
```  
  
 启动任务，等待它，您可以开始其他任务。 其他任务隐式并行运行，但创建没有其他线程。  
  
 下面的程序启动三个异步 web 下载包，然后等待其调用它们的顺序。 请注意，当运行任务始终不按顺序他们要在其中创建，并等待完成的程序。 他们开始运行后，它们创建一个或多个任务完成之前方法到达 await 表达式。  
  
> [!NOTE]
>  若要完成此项目，您必须具有 Visual Studio 2012 或更高版本和.NET Framework 4.5 或更高版本安装在您的计算机上。  
  
 在同时启动多个任务的另一个示例，请参阅[如何︰ 扩展异步演练使用 Task.WhenAll (Visual Basic 中) 通过](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)。  
  
 您可以下载此示例中从代码[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkId=254906)。  
  
### <a name="to-set-up-the-project"></a>设置项目  
  
1.  若要创建一个 WPF 应用程序，请完成以下步骤。 您可以找到有关这些步骤的详细的说明[演练︰ 使用 Async 和 Await (Visual Basic 中) 通过 Web 访问](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。  
  
    -   创建的 WPF 应用程序包含一个文本框和一个按钮。 将该按钮命名`startButton`，并命名为文本框中`resultsTextBox`。  
  
    -   添加<xref:System.Net.Http>。</xref:System.Net.Http>的引用  
  
    -   在 MainWindow.xaml.vb 文件中添加`Imports`语句`System.Net.Http`。  
  
### <a name="to-add-the-code"></a>添加代码  
  
1.  在设计窗口中，MainWindow.xaml，双击该按钮以创建`startButton_Click`MainWindow.xaml.vb 中的事件处理程序。  
  
2.  复制下面的代码，并将其粘贴到的正文`startButton_Click`MainWindow.xaml.vb 中。  
  
    ```vb  
    resultsTextBox.Clear()  
    Await CreateMultipleTasksAsync()  
    resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    ```  
  
     该代码调用异步方法， `CreateMultipleTasksAsync`，其中驱动应用程序。  
  
3.  向项目中添加以下支持方法︰  
  
    -   `ProcessURLAsync`使用<xref:System.Net.Http.HttpClient>方法以下载网站作为字节数组的内容。</xref:System.Net.Http.HttpClient> 支持的方法中，`ProcessURLAsync`然后显示，并返回数组的长度。  
  
    -   `DisplayResults`显示每个 URL 的字节数组中的字节数。 在每个任务已经完成下载时，这将显示所示。  
  
     将以下方法中，复制并粘贴它们后`startButton_Click`MainWindow.xaml.vb 中的事件处理程序。  
  
    ```vb  
    Private Async Function ProcessURLAsync(url As String, client As HttpClient) As Task(Of Integer)  
  
        Dim byteArray = Await client.GetByteArrayAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
  
    Private Sub DisplayResults(url As String, content As Byte())  
  
        ' Display the length of each website. The string format   
        ' is designed to be used with a monospaced font, such as  
        ' Lucida Console or Global Monospace.  
        Dim bytes = content.Length  
        ' Strip off the "http://".  
        Dim displayURL = url.Replace("http://", "")  
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)  
    End Sub  
    ```  
  
4.  最后，可以定义方法`CreateMultipleTasksAsync`，这将执行以下步骤。  
  
    -   该方法声明`HttpClient`对象，您需要访问方法<xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>中`ProcessURLAsync`。</xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>  
  
    -   该方法创建并启动三个任务类型的<xref:System.Threading.Tasks.Task%601>，其中`TResult`是一个整数。</xref:System.Threading.Tasks.Task%601> 每个任务完成后，如`DisplayResults`显示任务的 URL 和下载内容的长度。 因为任务以异步方式运行，结果的顺序可能与声明它们的顺序不同。  
  
    -   该方法等待每个任务的完成。 每个`Await`运算符暂停执行`CreateMultipleTasksAsync`直到所等待的任务完成。 运算符还会检索返回值通过调用`ProcessURLAsync`从每个已完成的任务。  
  
    -   当任务已完成并已检索的整数值时，该方法对求和的网站的长度，并显示结果。  
  
     复制下面的方法，并将其粘贴到您的解决方案。  
  
    ```vb  
    Private Async Function CreateMultipleTasksAsync() As Task  
  
        ' Declare an HttpClient object, and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Create and start the tasks. As each task finishes, DisplayResults   
        ' displays its length.  
        Dim download1 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com", client)  
        Dim download2 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client)  
        Dim download3 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client)  
  
        ' Await each task.  
        Dim length1 As Integer = Await download1  
        Dim length2 As Integer = Await download2  
        Dim length3 As Integer = Await download3  
  
        Dim total As Integer = length1 + length2 + length3  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
    ```  
  
5.  按 F5 键以运行程序，然后选择 **“启动”** 按钮。  
  
     多次运行该程序以验证以下三项任务不总是完成相同的顺序并在其中完成的顺序不一定的顺序在其中创建和等待。  
  
## <a name="example"></a>示例  
 下面的代码包含完整的示例。  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
        resultsTextBox.Clear()  
        Await CreateMultipleTasksAsync()  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Private Async Function CreateMultipleTasksAsync() As Task  
  
        ' Declare an HttpClient object, and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Create and start the tasks. As each task finishes, DisplayResults   
        ' displays its length.  
        Dim download1 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com", client)  
        Dim download2 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client)  
        Dim download3 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client)  
  
        ' Await each task.  
        Dim length1 As Integer = Await download1  
        Dim length2 As Integer = Await download2  
        Dim length3 As Integer = Await download3  
  
        Dim total As Integer = length1 + length2 + length3  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Async Function ProcessURLAsync(url As String, client As HttpClient) As Task(Of Integer)  
  
        Dim byteArray = Await client.GetByteArrayAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
  
    Private Sub DisplayResults(url As String, content As Byte())  
  
        ' Display the length of each website. The string format   
        ' is designed to be used with a monospaced font, such as  
        ' Lucida Console or Global Monospace.  
        Dim bytes = content.Length  
        ' Strip off the "http://".  
        Dim displayURL = url.Replace("http://", "")  
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)  
    End Sub  
End Class  
```  
  
## <a name="see-also"></a>另请参阅  
 [演练︰ 访问 Web 使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [异步编程使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [如何︰ 使用 Task.WhenAll (Visual Basic 中) 扩展异步演练](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)

