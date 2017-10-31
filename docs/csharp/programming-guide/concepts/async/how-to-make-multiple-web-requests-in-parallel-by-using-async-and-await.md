---
title: "如何：使用 Async 和 Await 并行发起多个 Web 请求 (C#)"
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
ms.assetid: 19745899-f97a-4499-a7c7-e813d1447580
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
ms.openlocfilehash: bfa7781241b837f353fe34d43b8cc6ab82f15564
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await-c"></a>如何：使用 Async 和 Await 并行发起多个 Web 请求 (C#)
在 async 方法中，任务在创建后即启动。 在任务完成前处理无法继续的方法中将 [await](../../../../csharp/language-reference/keywords/await.md) 运算符应用于任务。 通常任务被创建后即等待，如下面的示例所示。  
  
```csharp  
var result = await someWebAccessMethodAsync(url);  
```  
  
 但是，如果程序有其他不依赖于任务的完成的工作要完成，则可以将创建任务和等待任务分开。  
  
```csharp  
// The following line creates and starts the task.  
var myTask = someWebAccessMethodAsync(url);  
  
// While the task is running, you can do other work that doesn't depend  
// on the results of the task.  
// . . . . .  
  
// The application of await suspends the rest of this method until the task is complete.  
var result = await myTask;  
```  
  
 在启动任务和等待任务之间，可以启动其他任务。 其他任务以并行方式隐式运行，但不会创建其他线程。  
  
 下面的程序启动三个异步 Web 下载任务，然后按照任务的调用顺序等待其完成。 请注意，运行此程序时，任务并不总是按照创建和等待它们的顺序完成。 任务在创建后开始运行，在此方法到达 await 表达式之前可能已完成一个或多个任务。  
  
> [!NOTE]
>  若要完成此项目，计算机上必须安装有 Visual Studio 2012 或更高版本和 .NET Framework 4.5 或更高版本。  
  
 有关同时启动多个任务的其他示例，请参阅[如何：使用 Task.WhenAll 扩展异步演练 (C#)](../../../../csharp/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)。  
  
 可以从[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkId=254906)下载此示例的代码。  
  
### <a name="to-set-up-the-project"></a>设置项目  
  
1.  若要设置 WPF 应用程序，请完成以下步骤。 你可以在[演练：使用 Async 和 Await 访问 Web (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md) 中找到有关这些步骤的详细说明。  
  
    -   创建包含一个文本框和一个按钮的 WPF 应用程序。 将按钮命名为 `startButton`，将文本框命名为 `resultsTextBox`。  
  
    -   对 <xref:System.Net.Http> 添加引用。  
  
    -   在 MainWindow.xaml.cs 文件中添加用于 `System.Net.Http` 的 `using` 指令。  
  
### <a name="to-add-the-code"></a>添加代码  
  
1.  在设计窗口的 MainWindow.xaml 中，双击按钮以在 MainWindow.xaml.cs 中创建 `startButton_Click` 事件处理程序。  
  
2.  复制以下代码并粘贴到 MainWindow.xaml.cs 中的 `startButton_Click` 的正文中。  
  
    ```csharp  
    resultsTextBox.Clear();  
    await CreateMultipleTasksAsync();  
    resultsTextBox.Text += "\r\n\r\nControl returned to startButton_Click.\r\n";  
    ```  
  
     此代码调用异步方法 `CreateMultipleTasksAsync`，此方法驱动应用程序。  
  
3.  向项目中添加以下支持方法：  
  
    -   `ProcessURLAsync` 使用 <xref:System.Net.Http.HttpClient> 方法将网站内容下载为字节数组。 支持方法 `ProcessURLAsync` 随后显示并返回数组的长度。  
  
    -   `DisplayResults` 显示每个 URL 的字节数组中的字节数。 当所有任务完成下载后显示。  
  
     复制以下方法，并将它们粘贴在 MainWindow.xaml.cs 中的 `startButton_Click` 事件处理程序后面。  
  
    ```csharp  
    async Task<int> ProcessURLAsync(string url, HttpClient client)  
    {  
        var byteArray = await client.GetByteArrayAsync(url);  
        DisplayResults(url, byteArray);  
        return byteArray.Length;  
    }  
  
    private void DisplayResults(string url, byte[] content)  
    {  
        // Display the length of each website. The string format   
        // is designed to be used with a monospaced font, such as  
        // Lucida Console or Global Monospace.  
        var bytes = content.Length;  
        // Strip off the "http://".  
        var displayURL = url.Replace("http://", "");  
        resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
    }  
    ```  
  
4.  最后，定义方法 `CreateMultipleTasksAsync`，用于执行以下步骤。  
  
    -   该方法声明 `HttpClient` 对象，这需要你访问 `ProcessURLAsync` 中的 <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> 方法。  
  
    -   此方法创建并启动三个类型为 <xref:System.Threading.Tasks.Task%601> 的任务，其中 `TResult` 是一个整数。 每个任务完成后，`DisplayResults` 显示任务的 URL 和下载内容的长度。 由于任务是异步运行的，因此显示结果的顺序可能与声明任务的顺序不同。  
  
    -   此方法等待每个任务完成。 每个 `await` 运算符暂停执行 `CreateMultipleTasksAsync`，直到所等待的任务完成。 此运算符还会从每个已完成的任务的 `ProcessURLAsync` 调用中检索返回值。  
  
    -   当任务已完成并已检索到整数值时，此方法对网站的长度求和，并显示结果。  
  
     复制下面的方法，并将其粘贴到你的解决方案。  
  
    ```csharp  
    private async Task CreateMultipleTasksAsync()  
    {  
        // Declare an HttpClient object, and increase the buffer size. The  
        // default buffer size is 65,536.  
        HttpClient client =  
            new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
        // Create and start the tasks. As each task finishes, DisplayResults   
        // displays its length.  
        Task<int> download1 =   
            ProcessURLAsync("http://msdn.microsoft.com", client);  
        Task<int> download2 =   
            ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client);  
        Task<int> download3 =   
            ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client);  
  
        // Await each task.  
        int length1 = await download1;  
        int length2 = await download2;  
        int length3 = await download3;  
  
        int total = length1 + length2 + length3;  
  
        // Display the total count for the downloaded websites.  
        resultsTextBox.Text +=  
            string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
    }  
    ```  
  
5.  按 F5 键以运行程序，然后选择 **“启动”** 按钮。  
  
     多次运行此程序以确认三个任务并不总是以相同的顺序完成，并且完成的顺序不一定是创建和等待任务的顺序。  
  
## <a name="example"></a>示例  
 下面的代码包括完整的示例。  
  
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
  
// Add the following using directive, and add a reference for System.Net.Http.  
using System.Net.Http;  
  
namespace AsyncExample_MultipleTasks  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
            await CreateMultipleTasksAsync();  
            resultsTextBox.Text += "\r\n\r\nControl returned to startButton_Click.\r\n";  
        }  
  
        private async Task CreateMultipleTasksAsync()  
        {  
            // Declare an HttpClient object, and increase the buffer size. The  
            // default buffer size is 65,536.  
            HttpClient client =  
                new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
            // Create and start the tasks. As each task finishes, DisplayResults   
            // displays its length.  
            Task<int> download1 =   
                ProcessURLAsync("http://msdn.microsoft.com", client);  
            Task<int> download2 =   
                ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client);  
            Task<int> download3 =   
                ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client);  
  
            // Await each task.  
            int length1 = await download1;  
            int length2 = await download2;  
            int length3 = await download3;  
  
            int total = length1 + length2 + length3;  
  
            // Display the total count for the downloaded websites.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        async Task<int> ProcessURLAsync(string url, HttpClient client)  
        {  
            var byteArray = await client.GetByteArrayAsync(url);  
            DisplayResults(url, byteArray);  
            return byteArray.Length;  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each website. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "http://".  
            var displayURL = url.Replace("http://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [演练：使用 Async 和 Await 访问 Web (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [使用 Async 和 Await 的异步编程 (C#)](../../../../csharp/programming-guide/concepts/async/index.md)   
 [如何：使用 Task.WhenAll 扩展异步演练 (C#)](../../../../csharp/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)

