---
title: "启动多个异步任务并在其完成 (Visual Basic 中) 时处理 |Microsoft 文档"
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
ms.assetid: 57ffb748-af40-4794-bedd-bdb7fea062de
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
ms.openlocfilehash: 6fbf4611ecd64abfd016963dff887d82aad333b7
ms.lasthandoff: 03/13/2017

---
# <a name="start-multiple-async-tasks-and-process-them-as-they-complete-visual-basic"></a>启动多个异步任务并在其完成 (Visual Basic 中) 时处理
通过使用<xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName>，您可以同时启动多个任务和它们需要在完成而不是在启动它们的顺序处理这些处理它们逐个。</xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName>  
  
 下面的示例使用查询来创建任务的集合。 每个任务指定的网站的内容下载。 在一段时间每次迭代循环，等待的调用`WhenAny`先完成其下载的任务集合中返回的任务。 该任务是从集合中删除和处理。 循环重复，直到该集合不包含任何更多的任务。  
  
> [!NOTE]
>  若要运行的示例，必须具有 Visual Studio 2012 或更高版本和.NET Framework 4.5 或更高版本安装在您的计算机上。  
  
## <a name="downloading-the-example"></a>下载示例  
 您可以下载完整的 Windows Presentation Foundation (WPF) 项目，从[异步示例︰ 精细优化您的应用程序](http://go.microsoft.com/fwlink/?LinkId=255046)，然后按照这些步骤。  
  
1.  解压缩下载的文件，然后启动 Visual Studio。  
  
2.  在菜单栏上，依次选择 **“文件”**、 **“打开”**和 **“项目/解决方案”**。  
  
3.  在**打开项目**对话框中，打开保存的示例代码中您解压缩的文件夹，然后为 AsyncFineTuningVB 打开解决方案 (.sln) 文件。  
  
4.  在**解决方案资源管理器**，打开快捷菜单**ProcessTasksAsTheyFinish**项目，，然后选择**设为启动项目**。  
  
5.  选择 F5 键以运行该项目。  
  
     按 Ctrl + F5 键以运行该项目，不对其进行调试。  
  
6.  多次运行该项目以验证已下载的长度始终不会显示在相同的顺序。  
  
 如果您不想要下载的项目，你可以查看本主题末尾处的 MainWindow.xaml.vb 文件。  
  
## <a name="building-the-example"></a>生成示例  
 此示例将添加到代码中开发的[一个是否已完成 (Visual Basic 中) 后取消剩余异步任务](../../../../visual-basic/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md)，并使用相同的 UI。  
  
 若要生成示例自己执行的步骤，请按照"下载示例"部分中的说明进行操作，但选择**CancelAfterOneTask**作为**启动项目**。 将更改添加到本主题中`AccessTheWebAsync`在该项目中的方法。 所做的更改均标有星号。  
  
 **CancelAfterOneTask**项目已包含一个查询，在执行时，创建任务的集合。 每次调用`ProcessURLAsync`在下面的代码返回<xref:System.Threading.Tasks.Task%601>其中`TResult`是一个整数。</xref:System.Threading.Tasks.Task%601>  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 在项目的 MainWindow.xaml.vb 文件中，进行以下更改到`AccessTheWebAsync`方法。  
  
-   通过应用<xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>而不<xref:System.Linq.Enumerable.ToArray%2A>。</xref:System.Linq.Enumerable.ToArray%2A></xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>执行查询  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
-   添加一段时间将为集合中的每个任务执行以下步骤的循环。  
  
    1.  等待调用`WhenAny`来标识要完成的下载的集合的第一个任务。  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
    2.  从集合中删除该任务。  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
    3.  等待`firstFinishedTask`，通过调用返回`ProcessURLAsync`。 `firstFinishedTask`变量是<xref:System.Threading.Tasks.Task%601>其中`TReturn`是一个整数。</xref:System.Threading.Tasks.Task%601> 该任务已完成，但等待，如以下示例所示检索该下载网站的长度。  
  
        ```vb  
        Dim length = Await firstFinishedTask  
        resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
        ```  
  
 应多次运行该项目，以验证已下载的长度始终不会显示在相同的顺序。  
  
> [!CAUTION]
>  您可以使用`WhenAny`在循环中，该示例中，若要解决的问题，涉及少量的任务中所述。 但是，如果要处理大量任务，可以采用其他更高效的方法。 有关详细信息和示例，请参阅[处理任务，如它们完成](http://go.microsoft.com/fwlink/?LinkId=260810)。  
  
## <a name="complete-example"></a>完整的示例  
 下面的代码是该示例的 MainWindow.xaml.vb 文件的完整文本。 星号标记已针对此示例添加的元素。  
  
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
            resultsTextBox.Text &= vbCrLf & "Downloads complete."  
  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Downloads canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Downloads failed." & vbCrLf  
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
  
        ' ***Create a query that, when executed, returns a collection of tasks.  
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url, client, ct)  
  
        ' ***Use ToList to execute the query and start the download tasks.   
        Dim downloadTasks As List(Of Task(Of Integer)) = downloadTasksQuery.ToList()  
  
        ' ***Add a loop to process the tasks one at a time until none remain.  
        While downloadTasks.Count > 0  
            ' ***Identify the first task that completes.  
            Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
  
            ' ***Remove the selected task from the list so that you don't  
            ' process it more than once.  
            downloadTasks.Remove(firstFinishedTask)  
  
            ' ***Await the first completed task and display the results.  
            Dim length = Await firstFinishedTask  
            resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
        End While  
  
    End Function  
  
    ' Bundle the processing steps for a website into one async method.  
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
  
' Length of the download:  226093  
' Length of the download:  412588  
' Length of the download:  175490  
' Length of the download:  204890  
' Length of the download:  158855  
' Length of the download:  145790  
' Length of the download:  44908  
' Downloads complete.  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.Tasks.Task.WhenAny%2A></xref:System.Threading.Tasks.Task.WhenAny%2A>   
 [微调异步应用程序 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)   
 [异步编程使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [异步示例︰ 微调应用程序](http://go.microsoft.com/fwlink/?LinkId=255046)
