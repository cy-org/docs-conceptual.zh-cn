---
title: "使用 Async 以进行文件访问 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: c989305f-08e3-4687-95c3-948465cda202
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
ms.openlocfilehash: e0e548989b1d2c32b9faf5ce0dd90ae371dfc028
ms.lasthandoff: 03/13/2017

---
# <a name="using-async-for-file-access-visual-basic"></a>使用异步进行文件访问 (Visual Basic)
异步功能可用于访问文件。 通过使用异步功能，您可以调用异步方法而无需使用回调，也不需要跨多个方法或 lambda 表达式来拆分代码。 若要使同步代码异步，只需调用异步方法而不是一种同步方法中，并向代码中添加几个关键字。  
  
 你可以考虑将异步添加到文件访问调用由于以下原因︰  
  
-   异步使 UI 应用程序响应速度更快，因为启动该操作的 UI 线程可以执行其他操作。 如果 UI 线程必须执行的代码，需要很长时间 （例如超过 50 毫秒为单位），UI 可能会冻结，直到 I/O 完成并且 UI 线程可以再次处理键盘和鼠标输入和其他事件。  
  
-   异步通过减少线程的需要，可以提高 ASP.NET 的可伸缩性和其他基于服务器的应用程序。 如果应用程序使用每次响应的专用的线程，并且同时处理有&1000; 多个请求，则需要有&1000; 多个线程。 异步操作通常不需要使用一个线程在等待期间。 它们使用现有 I/O 完成线程短暂的结尾。  
  
-   文件访问操作的延迟可能会在当前条件下很低，但延迟可能会极大地提高了在将来。 例如，文件可能会移动到的服务器，则在世界各地。  
  
-   添加使用异步功能的开销很小。  
  
-   异步任务轻松地并行运行。  
  
## <a name="running-the-examples"></a>运行示例  
 若要运行本主题中的示例，可以创建**WPF 应用程序**或**Windows 窗体应用程序**，然后添加**按钮**。 在按钮的`Click`事件，每个示例中添加对第一种方法的调用。  
  
 在下面的示例中，包括以下`Imports`语句。  
  
```vb  
Imports System  
Imports System.Collections.Generic  
Imports System.Diagnostics  
Imports System.IO  
Imports System.Text  
Imports System.Threading.Tasks  
```  
  
## <a name="use-of-the-filestream-class"></a>使用 FileStream 类  
 在本主题使用示例<xref:System.IO.FileStream>类，该类包含一个选项，将导致异步 I/O，以在操作系统级别上发生。</xref:System.IO.FileStream> 通过使用此选项，可以避免阻塞线程池线程在许多情况下。 若要启用此选项，请指定`useAsync=true`或`options=FileOptions.Asynchronous`构造函数调用中的参数。  
  
 不能使用此选项<xref:System.IO.StreamReader>并且<xref:System.IO.StreamWriter>如果您打开它们直接通过指定文件路径。</xref:System.IO.StreamWriter> </xref:System.IO.StreamReader> 但是，您可以使用此选项，如果您为他们提供<xref:System.IO.Stream>，<xref:System.IO.FileStream>类打开。</xref:System.IO.FileStream> </xref:System.IO.Stream> 请注意，异步调用 UI 应用程序中更快即使线程池的线程被阻止，因为在等待期间不会阻止 UI 线程。  
  
## <a name="writing-text"></a>编写文本  
 下面的示例将文本写入文件。 在每个 await 语句，该方法立即退出。 文件 I/O 完成后，该方法恢复在 await 语句后面的语句处。 请注意，async 修饰符使用 await 语句的方法的定义中。  
  
```vb  
Public Async Sub ProcessWrite()  
    Dim filePath = "temp2.txt"  
    Dim text = "Hello World" & ControlChars.CrLf  
  
    Await WriteTextAsync(filePath, text)  
End Sub  
  
Private Async Function WriteTextAsync(filePath As String, text As String) As Task  
    Dim encodedText As Byte() = Encoding.Unicode.GetBytes(text)  
  
    Using sourceStream As New FileStream(filePath,  
        FileMode.Append, FileAccess.Write, FileShare.None,  
        bufferSize:=4096, useAsync:=True)  
  
        Await sourceStream.WriteAsync(encodedText, 0, encodedText.Length)  
    End Using  
End Function  
```  
  
 原始示例具有语句`Await sourceStream.WriteAsync(encodedText, 0, encodedText.Length)`，这是以下两个语句的缩写式︰  
  
```vb  
Dim theTask As Task = sourceStream.WriteAsync(encodedText, 0, encodedText.Length)  
Await theTask  
```  
  
 第一条语句返回一个任务，并会导致文件处理启动。 与 await 第二个语句会使方法立即退出并返回一个不同的任务。 完成处理更高版本的文件后，执行将返回到 await 后面的语句。 有关详细信息，请参阅[异步程序 (Visual Basic 中) 中的控制流](../../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)。  
  
## <a name="reading-text"></a>读取文本  
 下面的示例从文件读取文本。 文本要缓冲，这种情况下，将其放入<xref:System.Text.StringBuilder>。</xref:System.Text.StringBuilder> 与不同的是在上一示例中，await 表达式的计算生成的值。 <xref:System.IO.Stream.ReadAsync%2A>方法将返回<xref:System.Threading.Tasks.Task>\< <xref:System.Int32>1>，因此在等待的评估得出`Int32`值 (`numRead`) 操作完成后。</xref:System.Int32> </xref:System.Threading.Tasks.Task> </xref:System.IO.Stream.ReadAsync%2A> 有关详细信息，请参阅[异步返回类型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)。  
  
```vb  
Public Async Sub ProcessRead()  
    Dim filePath = "temp2.txt"  
  
    If File.Exists(filePath) = False Then  
        Debug.WriteLine("file not found: " & filePath)  
    Else  
        Try  
            Dim text As String = Await ReadTextAsync(filePath)  
            Debug.WriteLine(text)  
        Catch ex As Exception  
            Debug.WriteLine(ex.Message)  
        End Try  
    End If  
End Sub  
  
Private Async Function ReadTextAsync(filePath As String) As Task(Of String)  
  
    Using sourceStream As New FileStream(filePath,  
        FileMode.Open, FileAccess.Read, FileShare.Read,  
        bufferSize:=4096, useAsync:=True)  
  
        Dim sb As New StringBuilder  
  
        Dim buffer As Byte() = New Byte(&H1000) {}  
        Dim numRead As Integer  
        numRead = Await sourceStream.ReadAsync(buffer, 0, buffer.Length)  
        While numRead <> 0  
            Dim text As String = Encoding.Unicode.GetString(buffer, 0, numRead)  
            sb.Append(text)  
  
            numRead = Await sourceStream.ReadAsync(buffer, 0, buffer.Length)  
        End While  
  
        Return sb.ToString  
    End Using  
End Function  
```  
  
## <a name="parallel-asynchronous-io"></a>并行的异步 I/O  
 下面的示例演示通过编写 10 个文本文件的并行处理。 为每个文件<xref:System.IO.Stream.WriteAsync%2A>方法返回一个任务，然后添加到的任务的列表。</xref:System.IO.Stream.WriteAsync%2A> `Await Task.WhenAll(tasks)`语句将退出方法和简历时文件处理的方法中完成的所有任务。  
  
 该示例将关闭所有<xref:System.IO.FileStream>实例`Finally`阻止任务完成后。</xref:System.IO.FileStream> 如果每个`FileStream`中改为创建`Imports`语句，`FileStream`任务完成之前可能进行释放。  
  
 请注意，任何性能提升几乎完全从并行处理和不的异步处理。 异步的优点是它不会占用多个线程，并且它不会占用用户界面线程。  
  
```vb  
Public Async Sub ProcessWriteMult()  
    Dim folder = "tempfolder\"  
    Dim tasks As New List(Of Task)  
    Dim sourceStreams As New List(Of FileStream)  
  
    Try  
        For index = 1 To 10  
            Dim text = "In file " & index.ToString & ControlChars.CrLf  
  
            Dim fileName = "thefile" & index.ToString("00") & ".txt"  
            Dim filePath = folder & fileName  
  
            Dim encodedText As Byte() = Encoding.Unicode.GetBytes(text)  
  
            Dim sourceStream As New FileStream(filePath,  
                FileMode.Append, FileAccess.Write, FileShare.None,  
                bufferSize:=4096, useAsync:=True)  
  
            Dim theTask As Task = sourceStream.WriteAsync(encodedText, 0, encodedText.Length)  
            sourceStreams.Add(sourceStream)  
  
            tasks.Add(theTask)  
        Next  
  
        Await Task.WhenAll(tasks)  
    Finally  
        For Each sourceStream As FileStream In sourceStreams  
            sourceStream.Close()  
        Next  
    End Try  
End Sub  
```  
  
 当使用<xref:System.IO.Stream.WriteAsync%2A>和<xref:System.IO.Stream.ReadAsync%2A>方法，您可以指定<xref:System.Threading.CancellationToken>，它可用于取消操作的中间流。</xref:System.Threading.CancellationToken> </xref:System.IO.Stream.ReadAsync%2A> </xref:System.IO.Stream.WriteAsync%2A> 有关详细信息，请参阅[微调异步应用程序 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)和[托管线程中的取消](http://msdn.microsoft.com/library/eea11fe5-d8b0-4314-bb5d-8a58166fb1c3)。  
  
## <a name="see-also"></a>另请参阅  
 [异步编程使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [异步返回类型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)   
 [异步程序 (Visual Basic 中) 中的控制流](../../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)
