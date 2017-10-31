---
title: "控制流中异步程序 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: b0443af7-c586-4cb0-b476-742ae4098a96
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
ms.openlocfilehash: 15e02fbc023db9ae2f3ee9f40598faa7c9c027a0
ms.lasthandoff: 03/13/2017

---
# <a name="control-flow-in-async-programs-visual-basic"></a>异步程序 (Visual Basic 中) 中的控制流
你可以编写和维护异步程序更轻松地使用`Async`和`Await`关键字。 但是，结果可能会让您大吃一惊如果您不了解您的程序的运行方式。 通过一个简单的异步程序，以显示当控件移动，从一种方法对另一台和哪些信息的控制流传输每次此主题跟踪。  
  
> [!NOTE]
>  `Async` 和 `Await` 关键字是在 Visual Studio 2012 中引入的。  
  
 一般情况下，将包含与异步代码的方法的标记[异步](../../../../visual-basic/language-reference/modifiers/async.md)修饰符。 在使用 async 修饰符标记的方法，您可以使用[Await (Visual Basic 中)](../../../../visual-basic/language-reference/operators/await-operator.md)运算符来指定该方法暂停以等待完成异步调用过程的位置。 有关详细信息，请参阅[使用 Async 和 Await (Visual Basic 中) 的异步编程](../../../../visual-basic/programming-guide/concepts/async/index.md)。  
  
 下面的示例使用异步方法以字符串形式指定的网站的内容下载并显示字符串的长度。 此示例包含以下两种方法。  
  
-   `startButton_Click`后者调用`AccessTheWebAsync`并显示结果。  
  
-   `AccessTheWebAsync`它作为字符串的网站的内容下载，并返回字符串的长度。 `AccessTheWebAsync`使用异步<xref:System.Net.Http.HttpClient>方法， <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>，以下载内容。</xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> </xref:System.Net.Http.HttpClient>  
  
 编号的显示行显示在整个程序来帮助你了解如何在程序运行，还将说明在被标记为每个点会发生什么情况的关键点。 显示行标记"ONE"通过"六个。" 标签表示在其中程序到达这些代码行的顺序。  
  
 下面的代码演示了该程序的概述。  
  
```vb  
Class MainWindow  
  
    Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click  
  
        ' ONE  
        Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()  
  
        ' FOUR  
        Dim contentLength As Integer = Await getLengthTask  
  
        ' SIX  
        ResultsTextBox.Text &=  
            String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)  
  
    End Sub  
  
    Async Function AccessTheWebAsync() As Task(Of Integer)  
  
        ' TWO  
        Dim client As HttpClient = New HttpClient()   
        Dim getStringTask As Task(Of String) =   
            client.GetStringAsync("http://msdn.microsoft.com")  
  
        ' THREE  
        Dim urlContents As String = Await getStringTask  
  
        ' FIVE  
        Return urlContents.Length  
    End Function  
  
End Class  
  
```  
  
 每个标记的位置中，"ONE"通过"六，"显示有关该程序的当前状态信息。 将生成以下输出。  
  
```  
  
ONE:   Entering startButton_Click.  
           Calling AccessTheWebAsync.  
  
TWO:   Entering AccessTheWebAsync.  
           Calling HttpClient.GetStringAsync.  
  
THREE: Back in AccessTheWebAsync.  
           Task getStringTask is started.  
           About to await getStringTask & return a Task<int> to startButton_Click.  
  
FOUR:  Back in startButton_Click.  
           Task getLengthTask is started.  
           About to await getLengthTask -- no caller to return to.  
  
FIVE:  Back in AccessTheWebAsync.  
           Task getStringTask is complete.  
           Processing the return statement.  
           Exiting from AccessTheWebAsync.  
  
SIX:   Back in startButton_Click.  
           Task getLengthTask is finished.  
           Result from AccessTheWebAsync is stored in contentLength.  
           About to display contentLength and exit.  
  
Length of the downloaded string: 33946.  
```  
  
## <a name="set-up-the-program"></a>设置程序  
 您可以从 MSDN 下载本主题使用的代码，或者您可以自行构建。  
  
> [!NOTE]
>  若要运行该示例，必须具有 Visual Studio 2012 或更高版本和.NET Framework 4.5 或更高版本安装在您的计算机上。  
  
### <a name="download-the-program"></a>下载程序  
 您可以下载的应用程序中的相应主题[异步示例︰ 异步程序中的控制流](http://go.microsoft.com/fwlink/?LinkId=255285)。 以下步骤打开并运行该程序。  
  
1.  解压缩下载的文件，然后启动 Visual Studio。  
  
2.  在菜单栏上，依次选择 **“文件”**、 **“打开”**和 **“项目/解决方案”**。  
  
3.  导航到保存已解压缩的示例代码的文件夹，打开解决方案 (.sln) 文件，然后选择 F5 键以生成并运行项目。  
  
### <a name="build-the-program-yourself"></a>您自行生成程序  
 下面的 Windows Presentation Foundation (WPF) 项目包含本主题的代码示例。  
  
 若要运行项目，请执行下列步骤：  
  
1.  启动 Visual Studio。  
  
2.  在菜单栏上，依次选择“文件” ****、“新建” ****、“项目” ****。  
  
     **“新建项目”** 对话框随即打开。  
  
3.  在**已安装的模板**窗格中，选择**Visual Basic**，然后选择**WPF 应用程序**从项目类型列表。  
  
4.  输入`AsyncTracer`作为项目的名称，然后选择**确定**按钮。  
  
     新项目将出现在**解决方案资源管理器**。  
  
5.  在 Visual Studio 代码编辑器中，选择 **“MainWindow.xaml”** 选项卡。  
  
     如果看不到选项卡，打开快捷菜单中的 MainWindow.xaml**解决方案资源管理器**，然后选择**查看代码**。  
  
6.  在**XAML** MainWindow.xaml 视图中，将代码替换为下面的代码。  
  
    ```vb  
    <Window  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" x:Class="MainWindow"  
        Title="Control Flow Trace" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="221,10,0,0" VerticalAlignment="Top" Width="75"/>  
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" TextWrapping="Wrap" VerticalAlignment="Bottom" Width="510" Height="265" FontFamily="Lucida Console" FontSize="10" VerticalScrollBarVisibility="Visible" d:LayoutOverrides="HorizontalMargin"/>  
  
        </Grid>  
    </Window>  
  
    ```  
  
     一个简单的窗口，其中包含一个文本框和一个按钮将出现在**设计**MainWindow.xaml 的视图。  
  
7.  添加<xref:System.Net.Http>。</xref:System.Net.Http>的引用  
  
8.  在**解决方案资源管理器**，MainWindow.xaml.vb，打开快捷菜单，然后选择**查看代码**。  
  
9. MainWindow.xaml.vb，下面的代码替换该代码。  
  
    ```vb  
    ' Add an Imports statement and a reference for System.Net.Http.  
    Imports System.Net.Http  
  
    Class MainWindow  
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click  
  
            ' The display lines in the example lead you through the control shifts.  
            ResultsTextBox.Text &= "ONE:   Entering StartButton_Click." & vbCrLf &  
                "           Calling AccessTheWebAsync." & vbCrLf  
  
            Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()  
  
            ResultsTextBox.Text &= vbCrLf & "FOUR:  Back in StartButton_Click." & vbCrLf &  
                "           Task getLengthTask is started." & vbCrLf &  
                "           About to await getLengthTask -- no caller to return to." & vbCrLf  
  
            Dim contentLength As Integer = Await getLengthTask  
  
            ResultsTextBox.Text &= vbCrLf & "SIX:   Back in StartButton_Click." & vbCrLf &  
                "           Task getLengthTask is finished." & vbCrLf &  
                "           Result from AccessTheWebAsync is stored in contentLength." & vbCrLf &  
                "           About to display contentLength and exit." & vbCrLf  
  
            ResultsTextBox.Text &=  
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)  
        End Sub  
  
        Async Function AccessTheWebAsync() As Task(Of Integer)  
  
            ResultsTextBox.Text &= vbCrLf & "TWO:   Entering AccessTheWebAsync."  
  
            ' Declare an HttpClient object.  
            Dim client As HttpClient = New HttpClient()  
  
            ResultsTextBox.Text &= vbCrLf & "           Calling HttpClient.GetStringAsync." & vbCrLf  
  
            ' GetStringAsync returns a Task(Of String).   
            Dim getStringTask As Task(Of String) = client.GetStringAsync("http://msdn.microsoft.com")  
  
            ResultsTextBox.Text &= vbCrLf & "THREE: Back in AccessTheWebAsync." & vbCrLf &  
                "           Task getStringTask is started."  
  
            ' AccessTheWebAsync can continue to work until getStringTask is awaited.  
  
            ResultsTextBox.Text &=  
                vbCrLf & "           About to await getStringTask & return a Task(Of Integer) to StartButton_Click." & vbCrLf  
  
            ' Retrieve the website contents when task is complete.  
            Dim urlContents As String = Await getStringTask  
  
            ResultsTextBox.Text &= vbCrLf & "FIVE:  Back in AccessTheWebAsync." &  
                vbCrLf & "           Task getStringTask is complete." &  
                vbCrLf & "           Processing the return statement." &  
                vbCrLf & "           Exiting from AccessTheWebAsync." & vbCrLf  
  
            Return urlContents.Length  
        End Function  
  
    End Class  
    ```  
  
10. 按 F5 键以运行程序，然后选择 **“启动”** 按钮。  
  
     应出现以下输出。  
  
    ```  
    ONE:   Entering startButton_Click.  
               Calling AccessTheWebAsync.  
  
    TWO:   Entering AccessTheWebAsync.  
               Calling HttpClient.GetStringAsync.  
  
    THREE: Back in AccessTheWebAsync.  
               Task getStringTask is started.  
               About to await getStringTask & return a Task<int> to startButton_Click.  
  
    FOUR:  Back in startButton_Click.  
               Task getLengthTask is started.  
               About to await getLengthTask -- no caller to return to.  
  
    FIVE:  Back in AccessTheWebAsync.  
               Task getStringTask is complete.  
               Processing the return statement.  
               Exiting from AccessTheWebAsync.  
  
    SIX:   Back in startButton_Click.  
               Task getLengthTask is finished.  
               Result from AccessTheWebAsync is stored in contentLength.  
               About to display contentLength and exit.  
  
    Length of the downloaded string: 33946.  
    ```  
  
## <a name="trace-the-program"></a>跟踪程序  
  
### <a name="steps-one-and-two"></a>步骤&1; 和步骤&2;  
 前两个显示线追踪的路径作为`startButton_Click`调用`AccessTheWebAsync`，和`AccessTheWebAsync`调用异步<xref:System.Net.Http.HttpClient>方法<xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>。</xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> </xref:System.Net.Http.HttpClient> 下图概述了在调用方法方法。  
  
 ![两个步骤](../../../../csharp/programming-guide/concepts/async/media/asynctrace-onetwo.png "AsyncTrace ONETWO")  
  
 两者的返回类型`AccessTheWebAsync`和`client.GetStringAsync`是<xref:System.Threading.Tasks.Task%601>。</xref:System.Threading.Tasks.Task%601> 有关`AccessTheWebAsync`，TResult 是一个整数。 有关`GetStringAsync`，TResult 为字符串。 有关异步方法的返回类型的详细信息，请参阅[异步返回类型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)。  
  
 在控制切换回调用方时，返回任务的异步方法返回一个任务实例。 控制从异步方法返回其调用方时`Await`运算符时遇到的调用的方法或调用的方法结束时。 标记为"3"到"6"的显示行跟踪过程的这一部分。  
  
### <a name="step-three"></a>步骤&3;  
 在`AccessTheWebAsync`，异步方法<xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>调用以下载目标网页的内容。</xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> 控制将返回从`client.GetStringAsync`到`AccessTheWebAsync`时`client.GetStringAsync`返回。  
  
 `client.GetStringAsync`方法返回的字符串分配给一个 task`getStringTask`变量中`AccessTheWebAsync`。 该示例程序中的以下行说明如何调用`client.GetStringAsync`和分配。  
  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
 您可以将任务视为由一个承诺`client.GetStringAsync`以最终产生实际字符串。 在此期间，如果`AccessTheWebAsync`有工作要做的承诺字符串并不依赖于`client.GetStringAsync`，可以继续的处理而`client.GetStringAsync`等待。 在示例中，以下行的输出，分别标记为"3"，表示执行独立工作的机会  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
 下面的语句中止进度`AccessTheWebAsync`时`getStringTask`等待。  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
 下图显示了从控制流`client.GetStringAsync`到分配给`getStringTask`和从创建`getStringTask`到 Await 运算符的应用程序。  
  
 ![第三步](../../../../csharp/programming-guide/concepts/async/media/asynctrace-three.png "AsyncTrace 三")  
  
 Await 表达式挂起`AccessTheWebAsync`直到`client.GetStringAsync`返回。 同时，控件返回到调用方`AccessTheWebAsync`， `startButton_Click`。  
  
> [!NOTE]
>  通常情况下，您应当立即 await 为异步方法调用。 例如，以下赋值可以将替换为前面的代码中创建，然后等待`getStringTask`:`Dim urlContents As String = Await client.GetStringAsync("http://msdn.microsoft.com")`  
>   
>  在本主题中，await 运算符应用更高版本以容纳标记通过计划的控制流的输出行。  
  
### <a name="step-four"></a>步骤&4;  
 已声明返回类型的`AccessTheWebAsync`是`Task(Of Integer)`。 因此，当`AccessTheWebAsync`被挂起，它将返回到整数的任务`startButton_Click`。 您应该了解，则返回的任务不是`getStringTask`。 返回的任务是一项新任务的整数，它表示要在挂起的方法中，完成的剩余`AccessTheWebAsync`。 该任务是从一个承诺`AccessTheWebAsync`可以在该任务已完成时生成一个整数。  
  
 下列语句将赋给此任务`getLengthTask`变量。  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
 如下所示`AccessTheWebAsync`，`startButton_Click`可以继续工作并不取决于异步任务的结果 (`getLengthTask`) 之前等待的 task。 下面的输出行表示该工作。  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
 在进度`startButton_Click`时挂起`getLengthTask`等待。 下面的赋值语句将挂起`startButton_Click`直到`AccessTheWebAsync`已完成。  
  
<CodeContentPlaceHolder>10</CodeContentPlaceHolder>  
 下图中箭头显示从中的 await 表达式的控制流`AccessTheWebAsync`对分配到的值`getLengthTask`后, 跟在正常处理`startButton_Click`直到`getLengthTask`等待。  
  
 ![第四步](../../../../csharp/programming-guide/concepts/async/media/asynctrace-four.png "AsyncTrace 四")  
  
### <a name="step-five"></a>步骤&5;  
 当`client.GetStringAsync`表明它已完成，以处理`AccessTheWebAsync`发布从挂起，可以继续通过 await 语句。 下面的输出行表示继续处理。  
  
<CodeContentPlaceHolder>11</CodeContentPlaceHolder>  
 操作数的 return 语句`urlContents.Length`，存储在任务的`AccessTheWebAsync`返回。 Await 表达式检索该值从`getLengthTask`中`startButton_Click`。  
  
 下图显示了后控制的转移`client.GetStringAsync`(和`getStringTask`) 都已完成。  
  
 ![第五步](../../../../csharp/programming-guide/concepts/async/media/asynctrace-five.png "AsyncTrace 五个")  
  
 `AccessTheWebAsync`运行到完成，并且控件返回到`startButton_Click`，它正在等待完成。  
  
### <a name="step-six"></a>步骤&6;  
 当`AccessTheWebAsync`发出信号表示它已完成，处理可以继续通过中的 await 语句`startButton_Async`。 事实上，该程序没有更多。  
  
 下面的输出行表示在处理恢复`startButton_Async`:  
  
<CodeContentPlaceHolder>12</CodeContentPlaceHolder>  
 Await 表达式从检索`getLengthTask`return 语句中的操作数的整数值`AccessTheWebAsync`。 下面的语句将该值赋予`contentLength`变量。  
  
<CodeContentPlaceHolder>13</CodeContentPlaceHolder>  
 下图显示从控件返回`AccessTheWebAsync`到`startButton_Click`。  
  
 ![第六步](../../../../csharp/programming-guide/concepts/async/media/asynctrace-six.png "AsyncTrace 六个")  
  
## <a name="see-also"></a>另请参阅  
 [异步编程使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [异步返回类型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)   
 [演练︰ 访问 Web 使用 Async 和 Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [异步示例︰ 异步程序 （C# 和 Visual Basic） 中的控制流](http://go.microsoft.com/fwlink/?LinkId=255285)
