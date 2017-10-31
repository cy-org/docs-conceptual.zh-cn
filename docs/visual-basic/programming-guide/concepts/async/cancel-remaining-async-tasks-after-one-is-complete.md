---
title: "异步任务取消剩余一个后完成 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: c928b5a1-622f-4441-8baf-adca1dde197f
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
ms.openlocfilehash: 1b70822edd972ac33614ab49faad6ff50b0e80b7
ms.lasthandoff: 03/13/2017

---
# <a name="cancel-remaining-async-tasks-after-one-is-complete-visual-basic"></a>异步任务取消剩余一个后完成 (Visual Basic)
通过使用<xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName>方法和<xref:System.Threading.CancellationToken>，您可以在一个任务完成后取消所有剩余任务。</xref:System.Threading.CancellationToken> </xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName> `WhenAny`方法采用的参数是任务的集合。 该方法开始的所有任务，并返回单个任务。 在集合中的任何任务完成后，单个任务已完成。  
  
 此示例演示如何结合使用取消标记`WhenAny`来占用的第一个任务完成的任务的集合，并用于取消剩余任务。 每个任务的形式下载网站的内容。 本示例显示的第一个下载完成的内容的长度，并取消其他下载内容。  
  
> [!NOTE]
>  若要运行的示例，必须具有 Visual Studio 2012 或更高版本和.NET Framework 4.5 或更高版本安装在您的计算机上。  
  
## <a name="downloading-the-example"></a>下载示例  
 您可以下载完整的 Windows Presentation Foundation (WPF) 项目，从[异步示例︰ 精细优化您的应用程序](http://go.microsoft.com/fwlink/?LinkId=255046)，然后按照这些步骤。  
  
1.  解压缩下载的文件，然后启动 Visual Studio。  
  
2.  在菜单栏上，依次选择 **“文件”**、 **“打开”**和 **“项目/解决方案”**。  
  
3.  在**打开项目**对话框中，打开保存的示例代码中您解压缩的文件夹，然后为 AsyncFineTuningVB 打开解决方案 (.sln) 文件。  
  
4.  在**解决方案资源管理器**，打开快捷菜单**CancelAfterOneTask**项目，，然后选择**设为启动项目**。  
  
5.  选择 F5 键以运行该项目。  
  
     按 Ctrl + F5 键以运行该项目，不对其进行调试。  
  
6.  运行程序多次以验证其他的下载完成第一次。  
  
 如果您不想要下载的项目，你可以查看本主题末尾处的 MainWindow.xaml.vb 文件。  
  
## <a name="building-the-example"></a>生成示例  
 本主题中的示例将添加到项目中开发的[取消一个异步任务或列表任务](http://msdn.microsoft.com/library/d6e4e801-df64-4705-98fc-df725a577fb0)若要取消的任务的列表。 该示例使用相同的 UI，尽管**取消**不显式使用按钮。  
  
 若要生成示例自己执行的步骤，请按照"下载示例"部分中的说明进行操作，但选择**CancelAListOfTasks**作为**启动项目**。 向该项目添加本主题中的所做的更改。  
  
 MainWindow.xaml.vb 文件中的**CancelAListOfTasks**项目中，通过将每个网站的处理步骤从中的循环移动开始转换`AccessTheWebAsync`与下面的异步方法。  
  
```vb  
' ***Bundle the processing steps for a website into one async method.  
Async Function ProcessURLAsync(url As String, client As HttpClient, ct As CancellationToken) As Task(Of Integer)  
  
    ' GetAsync returns a Task(Of HttpResponseMessage).   
    Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
    ' Retrieve the website contents from the HttpResponseMessage.  
    Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
    Return urlContents.Length  
End Function  
```  
  
 在`AccessTheWebAsync`，此示例使用一个查询，<xref:System.Linq.Enumerable.ToArray%2A>方法，与`WhenAny`方法创建并启动任务的数组。</xref:System.Linq.Enumerable.ToArray%2A> 应用程序的`WhenAny`数组时将返回到一项任务，处于等待状态，计算结果为第一项任务来访问数组中完成的任务。  
  
 进行中的以下更改`AccessTheWebAsync`。 星号标记的代码文件中的更改。  
  
1.  注释掉或删除该循环。  
  
2.  创建一个查询，在执行时，生成的常规任务的集合。 每次调用`ProcessURLAsync`返回<xref:System.Threading.Tasks.Task%601>其中`TResult`是一个整数。</xref:System.Threading.Tasks.Task%601>  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
3.  调用`ToArray`执行查询并启动任务。 应用程序的`WhenAny`方法在下一步将执行查询，并启动任务，而无需使用`ToArray`，但其他方法可能不会。 最安全的做法是明确强制执行查询。  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
4.  调用`WhenAny`上的任务的集合。 `WhenAny`返回`Task(Of Task(Of Integer))`或`Task<Task<int>>`。  也就是说，`WhenAny`评估的任务返回单个`Task(Of Integer)`或`Task<int>`时等待。 该单个任务将集合中要完成的第一个任务。 第一次已完成的任务分配给`firstFinishedTask`。 一种`firstFinishedTask`是<xref:System.Threading.Tasks.Task%601>其中`TResult`是一个整数，因为这是返回类型的`ProcessURLAsync`。</xref:System.Threading.Tasks.Task%601>  
  
```vb  
' ***Call WhenAny and then await the result. The task that finishes   
' first is assigned to firstFinishedTask.  
Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
```  
  
5.  在此示例中，您只的感兴趣先完成的任务。 因此，使用<xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=fullName>若要取消剩余任务。</xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=fullName>  
  
```vb  
' ***Cancel the rest of the downloads. You just want the first one.  
cts.Cancel()  
```  
  
6.  最后，await`firstFinishedTask`要检索的下载内容的长度。  
  
```vb  
Dim length = Await firstFinishedTask  
resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
```  
  
 运行程序多次以验证其他的下载完成第一次。  
  
## <a name="complete-example"></a>完整的示例  
 下面的代码是该示例的完整 MainWindow.xaml.vb 或 MainWindow.xaml.cs 文件。 星号标记已针对此示例添加的元素。  
  
 请注意，您必须添加<xref:System.Net.Http>。</xref:System.Net.Http>的引用  
  
 您可以下载的项目[异步示例︰ 精细优化您的应用程序](http://go.microsoft.com/fwlink/?LinkId=255046)。  
  
```vb  
' Add an Imports directive and a reference for System.Net.Http.  
Imports System.Net.Http  
  
' Add the following Imports directive for System.Threading.  
Imports System.Threading  
  
Class MainWindow  
  
    ' Declare a System.Threading.CancellationTokenSource.  
    Dim cts As CancellationTokenSource  
  
    Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)  
  
        ' Instantiate the CancellationTokenSource.  
        cts = New CancellationTokenSource()  
  
        resultsTextBox.Clear()  
  
        Try  
            Await AccessTheWebAsync(cts.Token)  
            resultsTextBox.Text &= vbCrLf & "Download complete."  
  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Download failed." & vbCrLf  
        End Try  
  
        ' Set the CancellationTokenSource to Nothing when the download is complete.  
        cts = Nothing  
    End Sub  
  
    ' You can still include a Cancel button if you want to.  
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)  
  
        If cts IsNot Nothing Then  
            cts.Cancel()  
        End If  
    End Sub  
  
    ' Provide a parameter for the CancellationToken.  
    ' Change the return type to Task because the method has no return statement.  
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task  
  
        Dim client As HttpClient = New HttpClient()  
  
        ' Call SetUpURLList to make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        '' Comment out or delete the loop.  
        ''For Each url In urlList  
        ''    ' GetAsync returns a Task(Of HttpResponseMessage).   
        ''    ' Argument ct carries the message if the Cancel button is chosen.   
        ''    ' Note that the Cancel button can cancel all remaining downloads.  
        ''    Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ''    ' Retrieve the website contents from the HttpResponseMessage.  
        ''    Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        ''    resultsTextBox.Text &=  
        ''        String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, urlContents.Length)  
        ''Next  
  
        ' ***Create a query that, when executed, returns a collection of tasks.  
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url, client, ct)  
  
        ' ***Use ToArray to execute the query and start the download tasks.   
        Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
  
        ' ***Call WhenAny and then await the result. The task that finishes   
        ' first is assigned to firstFinishedTask.  
        Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
  
        ' ***Cancel the rest of the downloads. You just want the first one.  
        cts.Cancel()  
  
        ' ***Await the first completed task and display the results  
        ' Run the program several times to demonstrate that different  
        ' websites can finish first.  
        Dim length = Await firstFinishedTask  
        resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
    End Function  
  
    ' ***Bundle the processing steps for a website into one async method.  
    Async Function ProcessURLAsync(url As String, client As HttpClient, ct As CancellationToken) As Task(Of Integer)  
  
        ' GetAsync returns a Task(Of HttpResponseMessage).   
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ' Retrieve the website contents from the HttpResponseMessage.  
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        Return urlContents.Length  
    End Function  
  
    ' Add a method that creates a list of web addresses.  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            }  
        Return urls  
    End Function  
  
End Class  
  
' Sample output:  
  
' Length of the downloaded website:  158856  
  
' Download complete.  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.Tasks.Task.WhenAny%2A></xref:System.Threading.Tasks.Task.WhenAny%2A>   
 [微调异步应用程序 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)   
 [异步编程使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [异步示例︰ 微调应用程序](http://go.microsoft.com/fwlink/?LinkId=255046)
