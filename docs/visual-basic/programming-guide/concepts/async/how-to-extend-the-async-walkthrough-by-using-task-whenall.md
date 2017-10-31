---
title: "如何︰ 使用 Task.WhenAll (Visual Basic 中) 扩展异步演练 |Microsoft 文档"
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
ms.assetid: c06d386d-e996-4da9-bf3d-05a3b6c0a258
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 46c5cb9328f2fa1a4ffc5116d318bc3286419e13
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-extend-the-async-walkthrough-by-using-taskwhenall-visual-basic"></a>如何︰ 使用 Task.WhenAll (Visual Basic 中) 扩展异步演练
您可以提高中的异步解决方案的性能[演练︰ 使用 Async 和 Await (Visual Basic 中) 通过 Web 访问](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)通过使用<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>方法。</xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> 此方法异步等待多个异步操作，表示为一系列的任务。  
  
 您可能已经注意到在本演练的网站下载以不同的速率。 有时在网站上找到的一个速度很慢，这会延迟所有剩余的下载。 当您在本演练中运行生成的异步解决方案后，您可以结束该程序轻松地如果不想等待，但更好的选择将开始在同一时间的所有下载，并允许更快地下载继续而无需等待延迟的一个。  
  
 您将应用`Task.WhenAll`方法任务的集合。 应用程序的`WhenAll`返回集合中的每个任务完成之后未完成一项任务。 显示的任务来并行运行，但创建没有其他线程。 可以按任意顺序完成的任务。  
  
> [!IMPORTANT]
>  下面的过程描述中开发的异步应用程序的扩展[演练︰ 使用 Async 和 Await (Visual Basic 中) 通过 Web 访问](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。 您可以通过完成本演练或下载中的代码中开发应用程序[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkId=255191)。  
>   
>  若要运行该示例，您必须具有 Visual Studio 2012 或更高版本安装在您的计算机上。  
  
### <a name="to-add-taskwhenall-to-your-geturlcontentsasync-solution"></a>向你的 GetURLContentsAsync 解决方案中添加 Task.WhenAll  
  
1.  添加`ProcessURLAsync`方法的第一个应用程序开发的[演练︰ 使用 Async 和 Await (Visual Basic 中) 通过 Web 访问](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。  
  
    -   如果下载中的代码[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkId=255191)，打开 AsyncWalkthrough 项目，然后添加`ProcessURLAsync`MainWindow.xaml.vb 文件。  
  
    -   如果通过完成本演练开发的代码，请添加`ProcessURLAsync`的应用程序包括`GetURLContentsAsync`方法。 此应用程序的 MainWindow.xaml.vb 文件是"完整的代码示例从演练"部分中的第一个示例。  
  
     `ProcessURLAsync`方法整合了正文中的操作`For Each`循环中`SumPageSizesAsync`在原始的演练。 该方法以异步方式对作为字节数组，指定的网站的内容下载然后显示并返回字节数组的长度。  
  
    ```vb  
    Private Async Function ProcessURLAsync(url As String) As Task(Of Integer)  
  
        Dim byteArray = Await GetURLContentsAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
    ```  
  
2.  注释掉或删除`For Each`循环中`SumPageSizesAsync`，如下面的代码所示。  
  
    ```vb  
    'Dim total = 0  
    'For Each url In urlList  
  
    '    Dim urlContents As Byte() = Await GetURLContentsAsync(url)  
  
    '    ' The previous line abbreviates the following two assignment statements.  
  
    '    ' GetURLContentsAsync returns a task. At completion, the task  
    '    ' produces a byte array.  
    '    'Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)  
    '    'Dim urlContents As Byte() = Await getContentsTask  
  
    '    DisplayResults(url, urlContents)  
  
    '    ' Update the total.  
    '    total += urlContents.Length  
    'Next  
    ```  
  
3.  创建任务的集合。 下面的代码定义[查询](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)，通过在执行时<xref:System.Linq.Enumerable.ToArray%2A>方法时，创建的每个网站的内容下载的任务的集合。</xref:System.Linq.Enumerable.ToArray%2A> 该查询进行求值时，会启动任务。  
  
     将以下代码添加到方法`SumPageSizesAsync`的声明后`urlList`。  
  
    ```vb  
    ' Create a query.   
    Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
        From url In urlList Select ProcessURLAsync(url)  
  
    ' Use ToArray to execute the query and start the download tasks.  
    Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
    ```  
  
4.  应用`Task.WhenAll`到集合的任务， `downloadTasks`。 `Task.WhenAll`返回任务的集合中的所有任务都完成时完成一项任务。  
  
     在下面的示例中，`Await`表达式等待完成单个任务`WhenAll`返回。 表达式计算结果为整数，其中每个整数是一个下载网站的长度的数组。 添加以下代码到`SumPageSizesAsync`，只是你在上一步中添加的代码之后。  
  
    ```vb  
    ' Await the completion of all the running tasks.  
    Dim lengths As Integer() = Await Task.WhenAll(downloadTasks)  
  
    '' The previous line is equivalent to the following two statements.  
    'Dim whenAllTask As Task(Of Integer()) = Task.WhenAll(downloadTasks)  
    'Dim lengths As Integer() = Await whenAllTask  
    ```  
  
5.  最后，使用<xref:System.Linq.Enumerable.Sum%2A>方法来对其求和的所有网站的长度。</xref:System.Linq.Enumerable.Sum%2A> 添加以下代码行到`SumPageSizesAsync`。  
  
    ```vb  
    Dim total = lengths.Sum()  
    ```  
  
### <a name="to-add-taskwhenall-to-the-httpclientgetbytearrayasync-solution"></a>向 HttpClient.GetByteArrayAsync 解决方案中添加 Task.WhenAll  
  
1.  添加以下版本的`ProcessURLAsync`到第二个应用程序中开发的[演练︰ 使用 Async 和 Await (Visual Basic 中) 通过 Web 访问](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。  
  
    -   如果下载中的代码[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkId=255191)，打开 AsyncWalkthrough_HttpClient 项目，然后添加`ProcessURLAsync`MainWindow.xaml.vb 文件。  
  
    -   如果通过完成本演练开发的代码，请添加`ProcessURLAsync`的应用程序使用`HttpClient.GetByteArrayAsync`方法。 此应用程序的 MainWindow.xaml.vb 文件是"完整的代码示例从演练"部分中的第二个示例。  
  
     `ProcessURLAsync`方法整合了正文中的操作`For Each`循环中`SumPageSizesAsync`在原始的演练。 该方法以异步方式对作为字节数组，指定的网站的内容下载然后显示并返回字节数组的长度。  
  
     从唯一的区别`ProcessURLAsync`在前面过程中的方法是使用<xref:System.Net.Http.HttpClient>实例， `client`。</xref:System.Net.Http.HttpClient>  
  
    ```vb  
    Private Async Function ProcessURLAsync(url As String, client As HttpClient) As Task(Of Integer)  
  
        Dim byteArray = Await client.GetByteArrayAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
    ```  
  
2.  注释掉或删除`For Each`循环中`SumPageSizesAsync`，如下面的代码所示。  
  
    ```vb  
    'Dim total = 0   
    'For Each url In urlList   
    '    ' GetByteArrayAsync returns a task. At completion, the task   
    '    ' produces a byte array.   
    '    Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)   
  
    '    ' The following two lines can replace the previous assignment statement.   
    '    'Dim getContentsTask As Task(Of Byte()) = client.GetByteArrayAsync(url)   
    '    'Dim urlContents As Byte() = Await getContentsTask   
  
    '    DisplayResults(url, urlContents)   
  
    '    ' Update the total.   
    '    total += urlContents.Length   
    'Next  
  
    ```  
  
3.  定义[查询](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)，通过在执行时<xref:System.Linq.Enumerable.ToArray%2A>方法时，创建的每个网站的内容下载的任务的集合。</xref:System.Linq.Enumerable.ToArray%2A> 该查询进行求值时，会启动任务。  
  
     将以下代码添加到方法`SumPageSizesAsync`的声明后`client`和`urlList`。  
  
    ```vb  
    ' Create a query.  
    Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
        From url In urlList Select ProcessURLAsync(url, client)  
  
    ' Use ToArray to execute the query and start the download tasks.  
    Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
    ```  
  
4.  接下来，应用`Task.WhenAll`到集合的任务， `downloadTasks`。 `Task.WhenAll`返回任务的集合中的所有任务都完成时完成一项任务。  
  
     在下面的示例中，`Await`表达式等待完成单个任务`WhenAll`返回。 完成后，`Await`表达式计算结果为整数，其中每个整数是一个下载网站的长度的数组。 添加以下代码到`SumPageSizesAsync`，只是你在上一步中添加的代码之后。  
  
    ```vb  
    ' Await the completion of all the running tasks.  
    Dim lengths As Integer() = Await Task.WhenAll(downloadTasks)  
  
    '' The previous line is equivalent to the following two statements.  
    'Dim whenAllTask As Task(Of Integer()) = Task.WhenAll(downloadTasks)  
    'Dim lengths As Integer() = Await whenAllTask  
    ```  
  
5.  最后，使用<xref:System.Linq.Enumerable.Sum%2A>方法以获取所有网站的长度之和。</xref:System.Linq.Enumerable.Sum%2A> 添加以下代码行到`SumPageSizesAsync`。  
  
    ```vb  
    Dim total = lengths.Sum()  
    ```  
  
### <a name="to-test-the-taskwhenall-solutions"></a>测试 Task.WhenAll 解决方案  
  
-   对于任一解决方案中，选择 F5 键以运行该程序，然后选择**启动**按钮。 输出应类似于中的异步解决方案的输出[演练︰ 使用 Async 和 Await (Visual Basic 中) 通过 Web 访问](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。 但请注意，在网站上找到以不同的顺序在每次显示。  
  
## <a name="example"></a>示例  
 下面的代码演示对使用的项目的扩充`GetURLContentsAsync`方法以从 web 下载内容。  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
Imports System.Net  
Imports System.IO  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
  
        resultsTextBox.Clear()  
  
        ' One-step async call.  
        Await SumPageSizesAsync()  
  
        '' Two-step async call.  
        'Dim sumTask As Task = SumPageSizesAsync()  
        'Await sumTask  
  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Private Async Function SumPageSizesAsync() As Task  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        ' Create a query.   
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url)  
  
        ' Use ToArray to execute the query and start the download tasks.  
        Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
  
        ' You can do other work here before awaiting.  
  
        ' Await the completion of all the running tasks.  
        Dim lengths As Integer() = Await Task.WhenAll(downloadTasks)  
  
        '' The previous line is equivalent to the following two statements.  
        'Dim whenAllTask As Task(Of Integer()) = Task.WhenAll(downloadTasks)  
        'Dim lengths As Integer() = Await whenAllTask  
  
        Dim total = lengths.Sum()  
  
        'Dim total = 0  
        'For Each url In urlList  
  
        '    Dim urlContents As Byte() = Await GetURLContentsAsync(url)  
  
        '    ' The previous line abbreviates the following two assignment statements.  
  
        '    ' GetURLContentsAsync returns a task. At completion, the task  
        '    ' produces a byte array.  
        '    'Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)  
        '    'Dim urlContents As Byte() = Await getContentsTask  
  
        '    DisplayResults(url, urlContents)  
  
        '    ' Update the total.  
        '    total += urlContents.Length  
        'NextNext  
  
        ' Display the total count for all of the web addresses.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/hh290136.aspx",  
                "http://msdn.microsoft.com/library/ee256749.aspx",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            }  
        Return urls  
    End Function  
  
    ' The actions from the foreach loop are moved to this async method.  
    Private Async Function ProcessURLAsync(url As String) As Task(Of Integer)  
  
        Dim byteArray = Await GetURLContentsAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
  
    Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())  
  
        ' The downloaded resource ends up in the variable named content.  
        Dim content = New MemoryStream()  
  
        ' Initialize an HttpWebRequest for the current URL.  
        Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)  
  
        ' Send the request to the Internet resource and wait for  
        ' the response.  
        Using response As WebResponse = Await webReq.GetResponseAsync()  
            ' Get the data stream that is associated with the specified URL.  
            Using responseStream As Stream = response.GetResponseStream()  
                ' Read the bytes in responseStream and copy them to content.    
                ' CopyToAsync returns a Task, not a Task<T>.  
                Await responseStream.CopyToAsync(content)  
            End Using  
        End Using  
  
        ' Return the result as a byte array.  
        Return content.ToArray()  
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
  
## <a name="example"></a>示例  
 下面的代码显示的项目的使用方法的扩展`HttpClient.GetByteArrayAsync`从 web 下载内容。  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
Imports System.Net  
Imports System.IO  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
  
        resultsTextBox.Clear()  
  
        '' One-step async call.  
        Await SumPageSizesAsync()  
  
        '' Two-step async call.  
        'Dim sumTask As Task = SumPageSizesAsync()  
        'Await sumTask  
  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Private Async Function SumPageSizesAsync() As Task  
  
        ' Declare an HttpClient object and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        ' Create a query.  
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url, client)  
  
        ' Use ToArray to execute the query and start the download tasks.  
        Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
  
        ' You can do other work here before awaiting.  
  
        ' Await the completion of all the running tasks.  
        Dim lengths As Integer() = Await Task.WhenAll(downloadTasks)  
  
        '' The previous line is equivalent to the following two statements.  
        'Dim whenAllTask As Task(Of Integer()) = Task.WhenAll(downloadTasks)  
        'Dim lengths As Integer() = Await whenAllTask  
  
        Dim total = lengths.Sum()  
  
        ''<snippet7>  
        'Dim total = 0  
        'For Each url In urlList  
        '    ' GetByteArrayAsync returns a task. At completion, the task  
        '    ' produces a byte array.  
        '    '<snippet31>  
        '    Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)  
        '    '</snippet31>  
  
        '    ' The following two lines can replace the previous assignment statement.  
        '    'Dim getContentsTask As Task(Of Byte()) = client.GetByteArrayAsync(url)  
        '    'Dim urlContents As Byte() = Await getContentsTask  
  
        '    DisplayResults(url, urlContents)  
  
        '    ' Update the total.  
        '    total += urlContents.Length  
        'NextNext  
  
        ' Display the total count for all of the web addresses.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "http://www.msdn.com",  
                "http://msdn.microsoft.com/library/hh290136.aspx",  
                "http://msdn.microsoft.com/library/ee256749.aspx",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            }  
        Return urls  
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
 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName></xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>   
 [演练︰ 访问 Web 使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
