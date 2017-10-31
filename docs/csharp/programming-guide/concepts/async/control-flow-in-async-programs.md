---
title: "异步程序中的控制流 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: fc92b08b-fe1d-4d07-84ab-5192fafe06bb
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 3bfb01f6825894b7388aebc1b92012b003c9e44c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="control-flow-in-async-programs-c"></a>异步程序中的控制流 (C#)
可以使用 `async` 和 `await` 关键字更加轻松地编写和维护异步程序。 但是，如果不了解程序的运行方式，结果可能会让你大吃一惊。 此主题通过一个简单的异步程序跟踪控制流，以显示控制从一种方法移动到另一种方法的情况，以及每次所传输的信息。  
  
> [!NOTE]
>  `async` 和 `await` 关键字是在 Visual Studio 2012 中引入的。  
  
 一般情况下，使用 [async (C#)](../../../../csharp/language-reference/keywords/async.md) 修饰符标记包含异步代码的方法。 在使用 async 修饰符标记的方法中，可以使用 [await (C#)](../../../../csharp/language-reference/keywords/await.md) 运算符来指定暂停该方法以等待调用的异步进程完成的位置。 有关详细信息，请参阅[使用 Async 和 Await 的异步编程 (C#)](../../../../csharp/programming-guide/concepts/async/index.md)。  
  
 下面的示例使用异步方法以字符串的形式下载指定网站的内容，并显示该字符串的长度。 此示例包含以下两种方法。  
  
-   `startButton_Click`，它调用 `AccessTheWebAsync` 并显示结果。  
  
-   `AccessTheWebAsync`，它以字符串的形式下载网站的内容，并返回该字符串的长度。 `AccessTheWebAsync` 使用异步 <xref:System.Net.Http.HttpClient> 方法 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> 来下载内容。  
  
 编号的显示行显示在整个程序的策略点处，以帮助你了解程序的运行方式和说明被标记的每个点处发生的情况。 显示行标记为“1”到“6”。 该标签表示程序到达这些代码行的顺序。  
  
 下面的代码显示该程序的概要。  
  
```csharp  
public partial class MainWindow : Window  
{  
    // . . .  
    private async void startButton_Click(object sender, RoutedEventArgs e)  
    {  
        // ONE  
        Task<int> getLengthTask = AccessTheWebAsync();  
  
        // FOUR  
        int contentLength = await getLengthTask;  
  
        // SIX  
        resultsTextBox.Text +=  
            String.Format("\r\nLength of the downloaded string: {0}.\r\n", contentLength);  
    }  
  
    async Task<int> AccessTheWebAsync()  
    {  
        // TWO  
        HttpClient client = new HttpClient();  
        Task<string> getStringTask =  
            client.GetStringAsync("http://msdn.microsoft.com");  
  
        // THREE                   
        string urlContents = await getStringTask;  
  
        // FIVE  
        return urlContents.Length;  
    }  
}  
```  
  
 每个标记位置（“1”到“6”）显示有关该程序的当前状态的信息。 将生成以下输出。  
  
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
 可以从 MSDN 下载本主题使用的代码，也可以自行生成该代码。  
  
> [!NOTE]
>  若要运行该示例，计算机上必须安装 Visual Studio 2012 或更高版本和 .NET Framework 4.5 或更高版本。  
  
### <a name="download-the-program"></a>下载程序  
 可以从[异步示例：异步程序中的控制流](http://go.microsoft.com/fwlink/?LinkId=255285)中下载此主题的应用程序。 以下步骤将打开并运行该程序。  
  
1.  解压缩下载的文件，然后启动 Visual Studio。  
  
2.  在菜单栏上，依次选择 **“文件”**、 **“打开”**和 **“项目/解决方案”**。  
  
3.  导航到保存已解压缩的示例代码的文件夹，打开解决方案 (.sln) 文件，然后选择 F5 键以生成并运行项目。  
  
### <a name="build-the-program-yourself"></a>您自行生成程序  
 以下 Windows Presentation Foundation (WPF) 项目包含本主题的代码示例。  
  
 若要运行项目，请执行下列步骤：  
  
1.  启动 Visual Studio。  
  
2.  在菜单栏上，依次选择“文件” 、“新建” 、“项目” 。  
  
     **“新建项目”** 对话框随即打开。  
  
3.  在“已安装的模板”窗格中，选择“Visual C#”，然后从项目类型列表选择“WPF 应用程序”。  
  
4.  输入 `AsyncTracer` 作为项目名称，然后选择“确定”按钮。  
  
     新项目将出现在“解决方案资源管理器”中。  
  
5.  在 Visual Studio 代码编辑器中，选择 **“MainWindow.xaml”** 选项卡。  
  
     如果此选项卡不可见，则在“解决方案资源管理器”中，打开 MainWindow.xaml 的快捷菜单，然后选择“查看代码”。  
  
6.  在 MainWindow.xaml 的“XAML”视图中，将代码替换为以下代码。  
  
    ```csharp  
    <Window  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" x:Class="AsyncTracer.MainWindow"  
            Title="Control Flow Trace" Height="350" Width="592">  
        <Grid>  
            <Button x:Name="startButton" Content="Start  
    " HorizontalAlignment="Left" Margin="250,10,0,0" VerticalAlignment="Top" Width="75" Height="24"  Click="startButton_Click" d:LayoutOverrides="GridBox"/>  
            <TextBox x:Name="resultsTextBox" HorizontalAlignment="Left" TextWrapping="Wrap" VerticalAlignment="Bottom" Width="576" Height="265" FontFamily="Lucida Console" FontSize="10" VerticalScrollBarVisibility="Visible" Grid.ColumnSpan="3"/>  
        </Grid>  
    </Window>  
    ```  
  
     MainWindow.xaml 的“设计”视图中将显示一个简单的窗口，其中包含一个文本框和一个按钮。  
  
7.  对 <xref:System.Net.Http> 添加引用。  
  
8.  在“解决方案资源管理器”中，打开 MainWindow.xaml.cs 的快捷菜单，然后选择“查看代码”。  
  
9. 在 MainWindow.xaml.cs 中，将代码替换为以下代码。  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.Threading.Tasks;  
    using System.Windows;  
    using System.Windows.Controls;  
    using System.Windows.Data;  
    using System.Windows.Documents;  
    using System.Windows.Input;  
    using System.Windows.Media;  
    using System.Windows.Media.Imaging;  
    using System.Windows.Navigation;  
    using System.Windows.Shapes;  
  
    // Add a using directive and a reference for System.Net.Http;  
    using System.Net.Http;  
  
    namespace AsyncTracer  
    {  
        public partial class MainWindow : Window  
        {  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
  
            private async void startButton_Click(object sender, RoutedEventArgs e)  
            {  
                // The display lines in the example lead you through the control shifts.  
                resultsTextBox.Text += "ONE:   Entering startButton_Click.\r\n" +  
                    "           Calling AccessTheWebAsync.\r\n";  
  
                Task<int> getLengthTask = AccessTheWebAsync();  
  
                resultsTextBox.Text += "\r\nFOUR:  Back in startButton_Click.\r\n" +  
                    "           Task getLengthTask is started.\r\n" +  
                    "           About to await getLengthTask -- no caller to return to.\r\n";  
  
                int contentLength = await getLengthTask;  
  
                resultsTextBox.Text += "\r\nSIX:   Back in startButton_Click.\r\n" +  
                    "           Task getLengthTask is finished.\r\n" +  
                    "           Result from AccessTheWebAsync is stored in contentLength.\r\n" +  
                    "           About to display contentLength and exit.\r\n";  
  
                resultsTextBox.Text +=  
                    String.Format("\r\nLength of the downloaded string: {0}.\r\n", contentLength);  
            }  
  
            async Task<int> AccessTheWebAsync()  
            {  
                resultsTextBox.Text += "\r\nTWO:   Entering AccessTheWebAsync.";  
  
                // Declare an HttpClient object.  
                HttpClient client = new HttpClient();  
  
                resultsTextBox.Text += "\r\n           Calling HttpClient.GetStringAsync.\r\n";  
  
                // GetStringAsync returns a Task<string>.   
                Task<string> getStringTask = client.GetStringAsync("http://msdn.microsoft.com");  
  
                resultsTextBox.Text += "\r\nTHREE: Back in AccessTheWebAsync.\r\n" +  
                    "           Task getStringTask is started.";  
  
                // AccessTheWebAsync can continue to work until getStringTask is awaited.  
  
                resultsTextBox.Text +=  
                    "\r\n           About to await getStringTask and return a Task<int> to startButton_Click.\r\n";  
  
                // Retrieve the website contents when task is complete.  
                string urlContents = await getStringTask;  
  
                resultsTextBox.Text += "\r\nFIVE:  Back in AccessTheWebAsync." +  
                    "\r\n           Task getStringTask is complete." +  
                    "\r\n           Processing the return statement." +  
                    "\r\n           Exiting from AccessTheWebAsync.\r\n";  
  
                return urlContents.Length;  
            }  
        }  
    }  
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
  
### <a name="steps-one-and-two"></a>步骤 1 和步骤 2  
 在 `startButton_Click` 调用 `AccessTheWebAsync` 及 `AccessTheWebAsync` 调用异步 <xref:System.Net.Http.HttpClient> 方法 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> 时，前两个显示行会跟踪路径。 下图概述了从方法到方法的调用。  
  
 ![步骤 1 和步骤 2](../../../../csharp/programming-guide/concepts/async/media/asynctrace-onetwo.png "AsyncTrace-ONETWO")  
  
 `AccessTheWebAsync` 和 `client.GetStringAsync` 的返回类型都是 <xref:System.Threading.Tasks.Task%601>。 对于 `AccessTheWebAsync`，TResult 是一个整数。 对于 `GetStringAsync`，TResult 是一个字符串。 有关异步方法返回类型的详细信息，请参阅[异步返回类型 (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md)。  
  
 在控制切换回调用方时，任务返回异步方法将返回一个任务实例。 在调用的方法中遇到 `await` 运算符或在调用的方法结束时，控制会从异步方法返回其调用方。 标记为“3”到“6”的显示行将跟踪过程的这一部分。  
  
### <a name="step-three"></a>步骤 3  
 在 `AccessTheWebAsync` 中，调用异步方法 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> 以下载目标网页的内容。 返回 `client.GetStringAsync` 时，控制将从 `client.GetStringAsync` 返回到 `AccessTheWebAsync`。  
  
 `client.GetStringAsync` 方法将返回分配给 `AccessTheWebAsync` 中的 `getStringTask` 变量的字符串任务。 该示例程序中的以下行说明了对 `client.GetStringAsync` 的调用和赋值。  
  
```csharp  
Task<string> getStringTask = client.GetStringAsync("http://msdn.microsoft.com");  
```  
  
 可以将任务视为 `client.GetStringAsync` 的一个承诺，用于最终生成实际字符串。 同时，如果 `AccessTheWebAsync` 有要执行的工作，且该工作不依赖于 `client.GetStringAsync` 中承诺的字符串，则可在 `client.GetStringAsync` 等待时继续此工作。 在示例中，以下标记为“3”的输出行表示执行独立工作的机会  
  
```  
THREE: Back in AccessTheWebAsync.  
           Task getStringTask is started.  
           About to await getStringTask & return a Task<int> to startButton_Click.  
```  
  
 当 `getStringTask` 处于等待状态时，下面的语句将暂停 `AccessTheWebAsync` 中的进度。  
  
```csharp  
string urlContents = await getStringTask;  
```  
  
 下图显示了从 `client.GetStringAsync` 到 `getStringTask` 的赋值和从 `getStringTask` 的创建到 await 运算符的应用程序的控制流。  
  
 ![步骤 3](../../../../csharp/programming-guide/concepts/async/media/asynctrace-three.png "AsyncTrace-Three")  
  
 Await 表达式将暂停 `AccessTheWebAsync`，直到返回 `client.GetStringAsync`。 同时，控件返回至 `AccessTheWebAsync` 的调用方 `startButton_Click`。  
  
> [!NOTE]
>  通常情况下，应立即等待对异步方法的调用。 例如，以下赋值可以替换前面创建的代码，然后等待 `getStringTask`：`string urlContents = await client.GetStringAsync("http://msdn.microsoft.com");`  
>   
>  在本主题中，稍后将应用 await 运算符，以容纳通过程序标记控制流的输出行。  
  
### <a name="step-four"></a>步骤 4  
 `AccessTheWebAsync` 的声明的返回类型是 `Task<int>`。 因此，当 `AccessTheWebAsync` 处于挂起状态时，它会将整数任务返回到 `startButton_Click`。 应该了解返回的任务不是 `getStringTask`。 返回的任务是一个新的整数任务，它表示挂起的方法 `AccessTheWebAsync` 中仍需完成的任务。 该任务是 `AccessTheWebAsync` 中的一个承诺，当任务完成时，将生成一个整数。  
  
 下列语句将此任务分配给 `getLengthTask` 变量。  
  
```csharp  
Task<int> getLengthTask = AccessTheWebAsync();  
```  
  
 如 `AccessTheWebAsync` 中一样，`startButton_Click` 可以继续执行不依赖于异步任务 (`getLengthTask`) 的结果的工作，直到该任务处于等待状态。 下面的输出行表示该工作。  
  
```  
FOUR:  Back in startButton_Click.  
           Task getLengthTask is started.  
           About to await getLengthTask -- no caller to return to.  
```  
  
 当 `getLengthTask` 处于等待状态时，`startButton_Click` 中的进度将挂起。 下面的赋值语句将挂起 `startButton_Click`，直到完成 `AccessTheWebAsync`。  
  
```csharp  
int contentLength = await getLengthTask;  
```  
  
 下图中的箭头显示控制流，该控制流从 `AccessTheWebAsync` 中的 await 表达式到 `getLengthTask` 的赋值值，后跟 `startButton_Click` 中的正常处理，直到 `getLengthTask` 处于等待状态。  
  
 ![步骤 4](../../../../csharp/programming-guide/concepts/async/media/asynctrace-four.png "AsyncTrace-FOUR")  
  
### <a name="step-five"></a>步骤 5  
 当 `client.GetStringAsync` 指示它已完成时，`AccessTheWebAsync` 中的处理将从挂起状态释放，且可以继续通过 await 语句。 下面的输出行表示继续处理。  
  
```  
FIVE:  Back in AccessTheWebAsync.  
           Task getStringTask is complete.  
           Processing the return statement.  
           Exiting from AccessTheWebAsync.  
```  
  
 return 语句 `urlContents.Length` 的操作数存储于 `AccessTheWebAsync` 返回的任务中。 Await 表达式从 `startButton_Click` 中的 `getLengthTask` 检索该值。  
  
 下图显示了完成 `client.GetStringAsync`（和 `getStringTask`）后控制的转移。  
  
 ![步骤 5](../../../../csharp/programming-guide/concepts/async/media/asynctrace-five.png "AsyncTrace-FIVE")  
  
 `AccessTheWebAsync` 将一直运行直到完成，且控制将返回到 `startButton_Click`，它正在等待完成。  
  
### <a name="step-six"></a>步骤 6  
 当 `AccessTheWebAsync` 指示它已完成时，处理可以继续通过 `startButton_Async` 中的 await 语句。 事实上，该程序没有更多可执行的操作。  
  
 下面的输出行表示 `startButton_Async` 中处理的恢复：  
  
```  
SIX:   Back in startButton_Click.  
           Task getLengthTask is finished.  
           Result from AccessTheWebAsync is stored in contentLength.  
           About to display contentLength and exit.  
```  
  
 Await 表达式从 `getLengthTask` 中检索为 `AccessTheWebAsync` 中 return 语句的操作数的整数值。 下面的语句将该值赋给 `contentLength` 变量。  
  
```csharp  
int contentLength = await getLengthTask;  
```  
  
 下图显示从 `AccessTheWebAsync` 到 `startButton_Click` 的控制的返回。  
  
 ![步骤 6](../../../../csharp/programming-guide/concepts/async/media/asynctrace-six.png "AsyncTrace-SIX")  
  
## <a name="see-also"></a>另请参阅  
 [使用 Async 和 Await 的异步编程 (C#)](../../../../csharp/programming-guide/concepts/async/index.md)   
 [异步返回类型 (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md)   
 [演练：使用 Async 和 Await 访问 Web (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Async Sample: Control Flow in Async Programs (C# and Visual Basic)](http://go.microsoft.com/fwlink/?LinkId=255285)（异步示例：异步程序中的控制流（C# 和 Visual Basic））

