---
title: "访问 Web 以 Async 和 Await (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: get-started-article
dev_langs:
- VB
ms.assetid: 84fd047f-fab8-4d89-8ced-104fb7310a91
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
ms.openlocfilehash: 643fff648336c664961ad7956308acbaea262f61
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-accessing-the-web-by-using-async-and-await-visual-basic"></a>演练：使用 Async 和 Await 访问 Web (Visual Basic)
您可以编写异步程序更轻松、 更直观地通过使用中引入的功能[!INCLUDE[vs_dev11_long](../../../../csharp/includes/vs_dev11_long_md.md)]。 你可以编写类似于同步代码的异步代码，并让编译器处理异步代码通常需要的疑难回调函数和延续。  
  
 有关异步功能的详细信息，请参阅[使用 Async 和 Await (Visual Basic 中) 的异步编程](../../../../visual-basic/programming-guide/concepts/async/index.md)。  
  
 本演练从对网站列表中的字节数进行求和的同步 Windows Presentation Foundation (WPF) 应用程序入手， 然后使用新功能将该应用程序转换为异步解决方案。  
  
 如果您不想自己生成应用程序，您可以下载"异步示例︰ 访问 Web 演练 （C# 和 Visual Basic）"从[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkId=255191)。  
  
 在本演练中，你将完成下列任务：  
  
-   [若要创建一个 WPF 应用程序](#CreateWPFApp)  
  
-   [若要设计简单的 WPF MainWindow](#MainWindow)  
  
-   [若要添加的引用](#AddRef)  
  
-   [若要添加必要的 Imports 语句](#ImportsState)  
  
-   [若要创建同步应用程序](#synchronous)  
  
-   [若要测试同步解决方案](#testSynch)  
  
-   [将 geturlcontents 转换为异步方法](#GetURLContents)  
  
-   [将 sumpagesizes 转换为异步方法](#SumPageSizes)  
  
-   [将 startbutton_click 转换为异步方法](#startButton)  
  
-   [若要测试异步解决方案](#testAsynch)  
  
-   [若要使用.NET Framework 方法替换方法 GetURLContentsAsync](#GetURLContentsAsync)  
  
-   [示例](#BKMK_CompleteCodeExamples)  
  
## <a name="prerequisites"></a>先决条件  
 必须在您的计算机上安装 visual Studio 2012 或更高版本。 有关详细信息，请参阅[Microsoft 网站](http://go.microsoft.com/fwlink/?LinkId=235233)。  
  
###  <a name="CreateWPFApp"></a>若要创建一个 WPF 应用程序  
  
1.  启动 Visual Studio。  
  
2.  在菜单栏上，依次选择“文件” ****、“新建” ****、“项目” ****。  
  
     **“新建项目”** 对话框随即打开。  
  
3.  在**已安装的模板**窗格中，选择 Visual Basic，然后选择**WPF 应用程序**从项目类型列表。  
  
4.  在**名称**文字框中，输入`AsyncExampleWPF`，然后选择**确定**按钮。  
  
     新项目将出现在**解决方案资源管理器**。  
  
##  <a name="BKMK_DesignWPFMainWin"></a>   
###  <a name="MainWindow"></a>若要设计简单的 WPF MainWindow  
  
1.  在 Visual Studio 代码编辑器中，选择 **“MainWindow.xaml”** 选项卡。  
  
2.  如果**工具箱**窗口不可见，请打开**视图**菜单上，然后选择**工具箱**。  
  
3.  添加**按钮**控件和一个**TextBox**控制转移到**MainWindow**窗口。  
  
4.  突出显示**TextBox**控件，然后在**属性**窗口中，设置以下值︰  
  
    -   设置**名称**属性设置为`resultsTextBox`。  
  
    -   设置**高度**属性设置为 250。  
  
    -   设置**宽度**属性设置为 500。  
  
    -   在**文本**选项卡上，指定等宽字体，例如黑控制台或全局等宽字体。  
  
5.  突出显示**按钮**控件，然后在**属性**窗口中，设置以下值︰  
  
    -   设置**名称**属性设置为`startButton`。  
  
    -   值更改**内容**属性从**按钮**到**启动**。  
  
6.  定位文本框和按钮，以便这两项出现在**MainWindow**窗口。  
  
     有关 WPF XAML 设计器的详细信息，请参阅[使用 XAML 设计器创建 UI](https://docs.microsoft.com/visualstudio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio)。  
  
##  <a name="BKMK_AddReference"></a>   
###  <a name="AddRef"></a>若要添加的引用  
  
1.  在**解决方案资源管理器**，突出显示您的项目的名称。  
  
2.  在菜单栏上依次选择**项目**，**添加引用**。  
  
     **引用管理器**对话框随即出现。  
  
3.  在对话框中的顶部，请验证您的项目针对.NET Framework 4.5 或更高版本。  
  
4.  在**程序集**区域中，选择**Framework**如果不已经选择。  
  
5.  在名称的列表，选择**System.Net.Http**复选框。  
  
6.  选择**确定**按钮以关闭对话框。  
  
##  <a name="BKMK_AddStatesandDirs"></a>   
###  <a name="ImportsState"></a>若要添加必要的 Imports 语句  
  
1.  在**解决方案资源管理器**，MainWindow.xaml.vb，打开快捷菜单，然后选择**查看代码**。  
  
2.  将以下代码添加`Imports`语句如果它们尚不存在的代码文件的顶部。  
  
    ```vb  
    Imports System.Net.Http  
    Imports System.Net  
    Imports System.IO  
    ```  
  
##  <a name="BKMK_CreatSynchApp"></a>   
###  <a name="synchronous"></a>若要创建同步应用程序  
  
1.  在设计窗口中，MainWindow.xaml，双击**启动**按钮以创建`startButton_Click`MainWindow.xaml.vb 中的事件处理程序。  
  
2.  在 MainWindow.xaml.vb，将下面的代码复制到的正文`startButton_Click`:  
  
    ```vb  
    resultsTextBox.Clear()  
    SumPageSizes()  
    resultsTextBox.Text &= vbCrLf & "Control returned to startButton_Click."  
    ```  
  
     代码调用驱动应用程序 `SumPageSizes` 的方法，并在控件返回到 `startButton_Click` 时显示一条消息。  
  
3.  该同步解决方案的代码包含以下四个方法：  
  
    -   `SumPageSizes`，从 `SetUpURLList` 获取网页 URL 列表并随后调用 `GetURLContents` 和 `DisplayResults` 以处理每个 URL。  
  
    -   `SetUpURLList`，生成并返回 Web 地址列表。  
  
    -   `GetURLContents`，下载每个网站的内容并将内容作为字节数组返回。  
  
    -   `DisplayResults`，显示每个 URL 的字节数组中的字节数。  
  
     复制以下四种方法，然后再粘贴它们下`startButton_Click`MainWindow.xaml.vb 中的事件处理程序︰  
  
    ```vb  
    Private Sub SumPageSizes()  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        Dim total = 0  
        For Each url In urlList  
            ' GetURLContents returns the contents of url as a byte array.  
            Dim urlContents As Byte() = GetURLContents(url)  
  
            DisplayResults(url, urlContents)  
  
            ' Update the total.  
            total += urlContents.Length  
        Next  
  
        ' Display the total count for all of the web addresses.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf & "Total bytes returned:  {0}" & vbCrLf, total)  
    End Sub  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "http://msdn.microsoft.com/library/windows/apps/br211380.aspx",  
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
  
    Private Function GetURLContents(url As String) As Byte()  
  
        ' The downloaded resource ends up in the variable named content.  
        Dim content = New MemoryStream()  
  
        ' Initialize an HttpWebRequest for the current URL.  
        Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)  
  
        ' Send the request to the Internet resource and wait for  
        ' the response.  
        ' Note: you can't use HttpWebRequest.GetResponse in a Windows Store app.  
        Using response As WebResponse = webReq.GetResponse()  
            ' Get the data stream that is associated with the specified URL.  
            Using responseStream As Stream = response.GetResponseStream()  
                ' Read the bytes in responseStream and copy them to content.    
                responseStream.CopyTo(content)  
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
    ```  
  
##  <a name="BKMK_TestSynchSol"></a>   
###  <a name="testSynch"></a>若要测试同步解决方案  
  
1.  按 F5 键以运行程序，然后选择 **“启动”** 按钮。  
  
     此时应显示类似于下列列表的输出。  
  
    ```  
  
    msdn.microsoft.com/library/windows/apps/br211380.aspx        383832  
    msdn.microsoft.com                                            33964  
    msdn.microsoft.com/library/hh290136.aspx               225793  
    msdn.microsoft.com/library/ee256749.aspx               143577  
    msdn.microsoft.com/library/hh290138.aspx               237372  
    msdn.microsoft.com/library/hh290140.aspx               128279  
    msdn.microsoft.com/library/dd470362.aspx               157649  
    msdn.microsoft.com/library/aa578028.aspx               204457  
    msdn.microsoft.com/library/ms404677.aspx               176405  
    msdn.microsoft.com/library/ff730837.aspx               143474  
  
    Total bytes returned:  1834802  
  
    Control returned to startButton_Click.  
  
    ```  
  
     请注意，显示计数需要几秒钟时间。 与此同时，在等待请求的资源下载时，UI 线程处于被阻止状态。 结果是，您不能移动、 最大化、 最小化，或甚至在您选择后关闭显示窗口**启动**按钮。 在字节计数开始显示之前，这些操作都会失败。 如果网站没有响应，将不会指示哪个网站失败。 甚至停止等待和关闭程序也会很困难。  
  
##  <a name="BKMK_ConvertGtBtArr"></a>   
###  <a name="GetURLContents"></a>将 geturlcontents 转换为异步方法  
  
1.  若要转换成一个异步解决方案的同步解决方案，以启动的最佳位置，是在`GetURLContents`因为对调用<xref:System.Net.HttpWebRequest>方法<xref:System.Net.HttpWebRequest.GetResponse%2A>和<xref:System.IO.Stream>方法<xref:System.IO.Stream.CopyTo%2A>是应用程序用来访问 web。</xref:System.IO.Stream.CopyTo%2A> </xref:System.IO.Stream> </xref:System.Net.HttpWebRequest.GetResponse%2A> </xref:System.Net.HttpWebRequest> .NET Framework 提供两种方法的异步版本，这让转换变得轻松。  
  
     有关详细信息的方法中使用的`GetURLContents`，请参阅<xref:System.Net.WebRequest>。</xref:System.Net.WebRequest>  
  
    > [!NOTE]
    >  在你按照本演练中的步骤进行操作的过程中，将出现多个编译器错误。 你可以忽略这些错误并继续演练。  
  
     更改中的第三行调用的方法`GetURLContents`从`GetResponse`对异步的基于任务的<xref:System.Net.WebRequest.GetResponseAsync%2A>方法。</xref:System.Net.WebRequest.GetResponseAsync%2A>  
  
    ```vb  
    Using response As WebResponse = webReq.GetResponseAsync()  
    ```  
  
2.  `GetResponseAsync`返回一种<xref:System.Threading.Tasks.Task%601>。</xref:System.Threading.Tasks.Task%601> 在这种情况下，*任务返回变量*， `TResult`，具有类型<xref:System.Net.WebResponse>。</xref:System.Net.WebResponse> 该任务是在请求的任务已下载且任务已完成运行后，生成实际 `WebResponse` 对象的承诺。  
  
     若要检索`WebResponse`值从任务时，请将应用[Await](../../../../visual-basic/language-reference/operators/await-operator.md)运算符以对调用`GetResponseAsync`，如下面的代码所示。  
  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
     `Await`运算符将暂停当前方法的执行`GetURLContents`，直到所等待的任务已完成。 同时，控制权返回给当前方法的调用方。 在此示例中，当前方法是 `GetURLContents`，调用方是 `SumPageSizes`。 任务完成时，承诺的 `WebResponse` 对象作为等待的任务的值生成，并分配给变量 `response`。  
  
     The previous statement can be separated into the following two statements to clarify what happens.  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
     对 `webReq.GetResponseAsync` 的调用返回 `Task(Of WebResponse)` 或 `Task<WebResponse>`。 则`Await`运算符应用于要检索的任务`WebResponse`值。  
  
     If your async method has work to do that doesn’t depend on the completion of the task, the method can continue with that work between these two statements, after the call to the async method and before the await operator is applied. For examples, see [How to: Make Multiple Web Requests in Parallel by Using Async and Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md) and [How to: Extend the Async Walkthrough by Using Task.WhenAll (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md).  
  
3.  由于你添加了`Await`上一步中的运算符，则编译器将发生错误。 可以仅在使用标记的方法中使用运算符[异步](../../../../visual-basic/language-reference/modifiers/async.md)修饰符。 当你重复转换步骤以使用对 `CopyToAsync` 的调用替换对 `CopyTo` 的调用时，请忽略该错误。  
  
    -   更改到<xref:System.IO.Stream.CopyToAsync%2A>。</xref:System.IO.Stream.CopyToAsync%2A>调用的方法的名称  
  
    -   `CopyTo` 或 `CopyToAsync` 方法复制字节到其参数 `content`，并且不返回有意义的值。 在同步版本中，对 `CopyTo` 的调用是不返回值的简单语句。 异步版本`CopyToAsync`，返回一种<xref:System.Threading.Tasks.Task>。</xref:System.Threading.Tasks.Task> 任务函数类似“Task(void)”，并让该方法能够等待。 应用 `Await` 或 `await` 到对 `CopyToAsync` 的调用，如下列代码所示。  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
         上一条语句缩写以下两行代码。  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
4.  `GetURLContents` 中仍需要完成的操作是调整方法签名。 您可以使用`Await`仅在使用标记的方法中的运算符[异步](../../../../visual-basic/language-reference/modifiers/async.md)修饰符。 添加修饰符来标记该方法为*async 方法*，如下面的代码所示。  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
5.  异步方法的返回类型也只能<xref:System.Threading.Tasks.Task>、 <xref:System.Threading.Tasks.Task%601>。</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task> 在 Visual Basic 中，方法必须为返回 `Task` 或 `Task(Of T)` 的 `Function`，或方法必须为 `Sub`。 通常情况下，`Sub`方法仅用于异步事件处理程序，其中`Sub`是必需的。 在其他情况下，您将使用`Task(T)`如果已完成的方法有[返回](../../../../visual-basic/language-reference/statements/return-statement.md)语句返回值的类型 T，并且你使用`Task`如果已完成的方法不返回有意义的值。  
  
     有关详细信息，请参阅[异步返回类型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)。  
  
     方法 `GetURLContents` 具有 return 语句，且该语句返回字节数组。 因此，异步版本的返回类型为 Task(T)，其中 T 为字节数组。 在方法签名中进行下列更改：  
  
    -   更改返回类型设置为`Task(Of Byte())`。  
  
    -   按照约定，异步方法的名称以“Async”结尾，因此，请重命名方法 `GetURLContentsAsync`。  
  
     下列代码显示这些更改。  
  
    ```vb  
    Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())  
    ```  
  
     进行这几处更改后，`GetURLContents` 到异步方法的转换完成。  
  
##  <a name="BKMK_ConvertSumPagSzs"></a>   
###  <a name="SumPageSizes"></a>将 sumpagesizes 转换为异步方法  
  
1.  为 `SumPageSizes` 重复之前过程中的步骤。 首先，将对 `GetURLContents` 的调用更改为异步调用。  
  
    -   将调用的方法的名称从 `GetURLContents` 更改为 `GetURLContentsAsync`（如果尚未执行此操作）。  
  
    -   应用`Await`给任务的`GetURLContentsAsync`返回以获取字节数组值。  
  
     下列代码显示这些更改。  
  
    ```vb  
    Dim urlContents As Byte() = Await GetURLContentsAsync(url)  
    ```  
  
     上一个分配缩写以下两行代码。  
  
    ```vb  
    ' GetURLContentsAsync returns a task. At completion, the task   
    ' produces a byte array.   
    'Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)   
    'Dim urlContents As Byte() = Await getContentsTask  
  
    ```  
  
2.  在方法签名中进行下列更改：  
  
    -   此方法标记`Async`修饰符。  
  
    -   将“Async”添加到方法名称。  
  
    -   这一次没有任务返回变量 T，因为 `SumPageSizesAsync` 不返回 T 的值。(该方法没有`Return`语句。)但是，该方法必须返回 `Task` 才能进行等待。 因此，更改中的方法类型`Sub`到`Function`。 函数的返回类型为 `Task`。  
  
     下列代码显示这些更改。  
  
    ```vb  
    Private Async Function SumPageSizesAsync() As Task  
    ```  
  
     从 `SumPageSizes` 到 `SumPageSizesAsync` 的转换完成。  
  
##  <a name="BKMK_Cnvrtbttn1"></a>   
###  <a name="startButton"></a>将 startbutton_click 转换为异步方法  
  
1.  在事件处理程序中，将调用的方法的名称从 `SumPageSizes` 更改为 `SumPageSizesAsync`（如果尚未执行此操作）。  
  
2.  由于 `SumPageSizesAsync` 是异步方法，请更改事件处理程序中的代码以等待结果。  
  
     对 `SumPageSizesAsync` 的调用反射对 `GetURLContentsAsync` 中的 `CopyToAsync` 的调用。 调用返回的是 `Task`，而不是 `Task(T)`。  
  
     与之前的过程一样，你可以使用一条语句或两条语句转换调用。 下列代码显示这些更改。  
  
    ```vb  
    '' One-step async call.  
    Await SumPageSizesAsync()  
  
    ' Two-step async call.  
    'Dim sumTask As Task = SumPageSizesAsync()  
    'Await sumTask  
    ```  
  
3.  若要防止意外重新输入该操作，在顶部添加以下语句`startButton_Click`禁用**启动**按钮。  
  
    ```vb  
    ' Disable the button until the operation is complete.  
    startButton.IsEnabled = False  
    ```  
  
     可以重新启用事件处理程序末尾的按钮。  
  
    ```vb  
    ' Reenable the button in case you want to run the operation again.  
    startButton.IsEnabled = True  
    ```  
  
     有关重入的详细信息，请参阅[处理异步应用程序 (Visual Basic 中) 中的重入](../../../../visual-basic/programming-guide/concepts/async/handling-reentrancy-in-async-apps.md)。  
  
4.  最后，添加`Async`修饰符声明，以便事件处理程序可以等待`SumPagSizesAsync`。  
  
    ```vb  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
    ```  
  
     通常情况下，事件处理程序的名称不会更改。 返回类型不更改为`Task`因为事件处理程序必须是`Sub`Visual Basic 中的过程。  
  
     项目从同步处理到异步处理的转换完成。  
  
##  <a name="BKMK_testAsynchSolution"></a>   
###  <a name="testAsynch"></a>若要测试异步解决方案  
  
1.  按 F5 键以运行程序，然后选择 **“启动”** 按钮。  
  
2.  此时应显示类似于同步解决方案的输出的输出。 但是，请注意下列差异。  
  
    -   处理完成后，所有结果不会同时出现。 例如，两个程序都在 `startButton_Click` 中包含一行可以清除文本框的代码。 其目的是为了清除运行间隔文本框中，如果您选择**启动**后个结果集已显示的第二个时间的按钮。 在同步版本中，下载完成且 UI 线程可以自由完成其他工作时，文本框在计数第二次显示之前即被清除。 在异步版本中，文本框中之后立即清除您选择**启动**按钮。  
  
    -   最重要的是，UI 线程在下载过程中未被阻止。 在 Web 资源下载、计数和显示期间，可以移动窗口或调整窗口大小。 如果其中一个网站运行缓慢或没有响应，您可以通过选择取消该操作**关闭**按钮 (在右上角的红色字段中 x)。  
  
##  <a name="BKMK_ReplaceGetByteArrayAsync"></a>   
###  <a name="GetURLContentsAsync"></a>若要使用.NET Framework 方法替换方法 GetURLContentsAsync  
  
1.  .NET Framework 4.5 提供可供你使用的许多异步方法。 其中之一，<xref:System.Net.Http.HttpClient>方法<xref:System.Net.Http.HttpClient.GetByteArrayAsync%28System.String%29>，没有正是您所需要对于本演练。</xref:System.Net.Http.HttpClient.GetByteArrayAsync%28System.String%29> </xref:System.Net.Http.HttpClient> 你可以使用它来替代你在早前过程中创建的 `GetURLContentsAsync` 方法。  
  
     第一步是在方法 `SumPageSizesAsync` 中创建 `HttpClient` 对象。 在方法的开头添加下列声明。  
  
    ```vb  
    ' Declare an HttpClient object and increase the buffer size. The  
    ' default buffer size is 65,536.  
    Dim client As HttpClient =  
        New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
    ```  
  
2.  在 `SumPageSizesAsync,` 中，使用对 `HttpClient` 方法的调用替换对 `GetURLContentsAsync` 方法的调用。  
  
    ```vb  
    Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)  
    ```  
  
3.  删除或注释禁用你编写的 `GetURLContentsAsync` 方法。  
  
4.  按 F5 键以运行程序，然后选择 **“启动”** 按钮。  
  
     此版本的项目的行为应与“测试异步解决方案”过程描述的行为匹配，且你的工作量应该更少。  
  
##  <a name="BKMK_CompleteCodeExamples"></a>示例  
 下列代码包含使用你编写的异步 `GetURLContentsAsync` 方法从同步解决方案转换为异步解决方案的完整示例。 请注意，它与原始同步解决方案十分类似。  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
Imports System.Net  
Imports System.IO  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
  
        ' Disable the button until the operation is complete.  
        startButton.IsEnabled = False  
  
        resultsTextBox.Clear()  
  
        '' One-step async call.  
        Await SumPageSizesAsync()  
  
        ' Two-step async call.  
        'Dim sumTask As Task = SumPageSizesAsync()  
        'Await sumTask  
  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
  
        ' Reenable the button in case you want to run the operation again.  
        startButton.IsEnabled = True  
    End Sub  
  
    Private Async Function SumPageSizesAsync() As Task  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        Dim total = 0  
        For Each url In urlList  
            Dim urlContents As Byte() = Await GetURLContentsAsync(url)  
  
            ' The previous line abbreviates the following two assignment statements.  
  
            '//<snippet21>  
            ' GetURLContentsAsync returns a task. At completion, the task  
            ' produces a byte array.  
            'Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)  
            'Dim urlContents As Byte() = Await getContentsTask  
  
            DisplayResults(url, urlContents)  
  
            ' Update the total.  
            total += urlContents.Length  
        Next  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "http://msdn.microsoft.com/library/windows/apps/br211380.aspx",  
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
  
    Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())  
  
        ' The downloaded resource ends up in the variable named content.  
        Dim content = New MemoryStream()  
  
        ' Initialize an HttpWebRequest for the current URL.  
        Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)  
  
        ' Send the request to the Internet resource and wait for  
        ' the response.  
        Using response As WebResponse = Await webReq.GetResponseAsync()  
  
            ' The previous statement abbreviates the following two statements.  
  
            'Dim responseTask As Task(Of WebResponse) = webReq.GetResponseAsync()  
            'Using response As WebResponse = Await responseTask  
  
            ' Get the data stream that is associated with the specified URL.  
            Using responseStream As Stream = response.GetResponseStream()  
                ' Read the bytes in responseStream and copy them to content.    
                Await responseStream.CopyToAsync(content)  
  
                ' The previous statement abbreviates the following two statements.  
  
                ' CopyToAsync returns a Task, not a Task<T>.  
                'Dim copyTask As Task = responseStream.CopyToAsync(content)  
  
                ' When copyTask is completed, content contains a copy of  
                ' responseStream.  
                'Await copyTask  
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
  
 下列代码包含使用 `HttpClient` 方法 `GetByteArrayAsync` 的解决方案的完整示例。  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
Imports System.Net  
Imports System.IO  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
  
        resultsTextBox.Clear()  
  
        ' Disable the button until the operation is complete.  
        startButton.IsEnabled = False  
  
        ' One-step async call.  
        Await SumPageSizesAsync()  
  
        '' Two-step async call.  
        'Dim sumTask As Task = SumPageSizesAsync()  
        'Await sumTask  
  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
  
        ' Reenable the button in case you want to run the operation again.  
        startButton.IsEnabled = True  
    End Sub  
  
    Private Async Function SumPageSizesAsync() As Task  
  
        ' Declare an HttpClient object and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        Dim total = 0  
        For Each url In urlList  
            ' GetByteArrayAsync returns a task. At completion, the task  
            ' produces a byte array.  
            Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)  
  
            ' The following two lines can replace the previous assignment statement.  
            'Dim getContentsTask As Task(Of Byte()) = client.GetByteArrayAsync(url)  
            'Dim urlContents As Byte() = Await getContentsTask  
  
            DisplayResults(url, urlContents)  
  
            ' Update the total.  
            total += urlContents.Length  
        Next  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "http://msdn.microsoft.com/library/windows/apps/br211380.aspx",  
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
 [异步示例︰ 访问 Web 演练 （C# 和 Visual Basic）](http://go.microsoft.com/fwlink/?LinkId=255191)   
 [Await 运算符](../../../../visual-basic/language-reference/operators/await-operator.md)   
 [异步](../../../../visual-basic/language-reference/modifiers/async.md)   
 [异步编程使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [异步返回类型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)   
 [基于任务的异步编程 (TAP)](http://go.microsoft.com/fwlink/?LinkId=204847)   
 [如何︰ 使用 Task.WhenAll (Visual Basic 中) 扩展异步演练](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)   
 [如何︰ 并行发起多个 Web 请求，使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md)
