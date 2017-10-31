---
title: "演练：利用 BackgroundWorker 组件进行多线程处理 (C#)"
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
ms.assetid: ff670fbf-a0ac-40c1-ab08-9ed53768f880
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
ms.openlocfilehash: 541a1ec788c337eea9965b8a46155e5c6606ea2f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="walkthrough-multithreading-with-the-backgroundworker-component-c"></a>演练：利用 BackgroundWorker 组件进行多线程处理 (C#)
本演练演示如何创建在文本文件中搜索单词出现次数的多线程 Windows 窗体应用程序。 演示内容包括：  
  
-   使用可由 <xref:System.ComponentModel.BackgroundWorker> 组件调用的方法定义类。  
  
-   处理 <xref:System.ComponentModel.BackgroundWorker> 组件引发的事件。  
  
-   启动 <xref:System.ComponentModel.BackgroundWorker> 组件运行方法。  
  
-   实现停止 <xref:System.ComponentModel.BackgroundWorker> 组件的 `Cancel` 按钮。  
  
### <a name="to-create-the-user-interface"></a>创建用户界面  
  
1.  打开新的 C# Windows 窗体应用程序项目，并创建名为 `Form1` 的窗体。  
  
2.  向 `Form1` 中添加两个按钮和四个文本框。  
  
3.  按下表所示命名对象。  
  
    |对象|属性|设置|  
    |------------|--------------|-------------|  
    |第一个按钮|`Name`, `Text`|启动，启动|  
    |第二个按钮|`Name`, `Text`|取消，取消|  
    |第一个文本框|`Name`, `Text`|SourceFile，""|  
    |第二个文本框|`Name`, `Text`|CompareString，""|  
    |第三个文本框|`Name`, `Text`|WordsCounted，"0"|  
    |第四个文本框|`Name`, `Text`|LinesCounted，"0"|  
  
4.  在每个文本框旁添加一个标签。 为每个标签设置 `Text` 属性，如下表所示。  
  
    |对象|属性|设置|  
    |------------|--------------|-------------|  
    |第一个标签|`Text`|源文件|  
    |第二个标签|`Text`|比较字符串|  
    |第三个标签|`Text`|匹配的单词|  
    |第四个标签|`Text`|行计数|  
  
### <a name="to-create-a-backgroundworker-component-and-subscribe-to-its-events"></a>创建 BackgroundWorker 组件并订阅其事件  
  
1.  从“工具箱”的“组件”部分，将 <xref:System.ComponentModel.BackgroundWorker> 组件添加到窗体。 它将出现在窗体的组件栏中。  
  
2.  为 backgroundWorker1 对象设置以下属性。  
  
    |属性|设置|  
    |--------------|-------------|  
    |`WorkerReportsProgress`|True|  
    |`WorkerSupportsCancellation`|True|  
  
3.  订阅 backgroundWorker1 对象的事件。 在“属性”窗口的顶部，单击“事件”图标。 双击 `RunWorkerCompleted` 事件，创建一个事件处理程序方法。 对 `ProgressChanged` 和 `DoWork` 事件执行相同操作。  
  
### <a name="to-define-the-method-that-will-run-on-a-separate-thread"></a>定义将在单独线程上运行的方法  
  
1.  在“项目”菜单中，选择“添加类”以将类添加到项目。 随即出现“添加新项”对话框。  
  
2.  从模板窗口选择“类”，然后在名称字段中输入 `Words.cs`。  
  
3.  单击 **“添加”**。 随即出现 `Words` 类。  
  
4.  将下面的代码添加到 `Words` 类中:  
  
    ```csharp  
    public class Words  
    {  
        // Object to store the current state, for passing to the caller.  
        public class CurrentState  
        {  
            public int LinesCounted;  
            public int WordsMatched;  
        }  
  
        public string SourceFile;  
        public string CompareString;  
        private int WordCount;  
        private int LinesCounted;  
  
        public void CountWords(  
            System.ComponentModel.BackgroundWorker worker,  
            System.ComponentModel.DoWorkEventArgs e)  
        {  
            // Initialize the variables.  
            CurrentState state = new CurrentState();  
            string line = "";  
            int elapsedTime = 20;  
            DateTime lastReportDateTime = DateTime.Now;  
  
            if (CompareString == null ||  
                CompareString == System.String.Empty)  
            {  
                throw new Exception("CompareString not specified.");  
            }  
  
            // Open a new stream.  
            using (System.IO.StreamReader myStream = new System.IO.StreamReader(SourceFile))  
            {  
                // Process lines while there are lines remaining in the file.  
                while (!myStream.EndOfStream)  
                {  
                    if (worker.CancellationPending)  
                    {  
                        e.Cancel = true;  
                        break;  
                    }  
                    else  
                    {  
                        line = myStream.ReadLine();  
                        WordCount += CountInString(line, CompareString);  
                        LinesCounted += 1;  
  
                        // Raise an event so the form can monitor progress.  
                        int compare = DateTime.Compare(  
                            DateTime.Now, lastReportDateTime.AddMilliseconds(elapsedTime));  
                        if (compare > 0)  
                        {  
                            state.LinesCounted = LinesCounted;  
                            state.WordsMatched = WordCount;  
                            worker.ReportProgress(0, state);  
                            lastReportDateTime = DateTime.Now;  
                        }  
                    }  
                    // Uncomment for testing.  
                    //System.Threading.Thread.Sleep(5);  
                }  
  
                // Report the final count values.  
                state.LinesCounted = LinesCounted;  
                state.WordsMatched = WordCount;  
                worker.ReportProgress(0, state);  
            }  
        }  
  
        private int CountInString(  
            string SourceString,  
            string CompareString)  
        {  
            // This function counts the number of times  
            // a word is found in a line.  
            if (SourceString == null)  
            {  
                return 0;  
            }  
  
            string EscapedCompareString =  
                System.Text.RegularExpressions.Regex.Escape(CompareString);  
  
            System.Text.RegularExpressions.Regex regex;  
            regex = new System.Text.RegularExpressions.Regex(   
                // To count all occurrences of the string, even within words, remove  
                // both instances of @"\b" from the following line.  
                @"\b" + EscapedCompareString + @"\b",  
                System.Text.RegularExpressions.RegexOptions.IgnoreCase);  
  
            System.Text.RegularExpressions.MatchCollection matches;  
            matches = regex.Matches(SourceString);  
            return matches.Count;  
        }  
  
    }  
    ```  
  
### <a name="to-handle-events-from-the-thread"></a>处理线程中的事件  
  
-   将以下事件处理程序添加到主窗体：  
  
    ```csharp  
    private void backgroundWorker1_RunWorkerCompleted(object sender, RunWorkerCompletedEventArgs e)  
    {  
    // This event handler is called when the background thread finishes.  
    // This method runs on the main thread.  
    if (e.Error != null)  
        MessageBox.Show("Error: " + e.Error.Message);  
    else if (e.Cancelled)  
        MessageBox.Show("Word counting canceled.");  
    else  
        MessageBox.Show("Finished counting words.");  
    }  
  
    private void backgroundWorker1_ProgressChanged(object sender, ProgressChangedEventArgs e)  
    {  
        // This method runs on the main thread.  
        Words.CurrentState state =  
            (Words.CurrentState)e.UserState;  
        this.LinesCounted.Text = state.LinesCounted.ToString();  
        this.WordsCounted.Text = state.WordsMatched.ToString();  
    }  
    ```  
  
### <a name="to-start-and-call-a-new-thread-that-runs-the-wordcount-method"></a>启动和调用运行 WordCount 方法的新线程  
  
1.  将下面的过程添加到程序中：  
  
    ```csharp  
    private void backgroundWorker1_DoWork(object sender, DoWorkEventArgs e)  
    {  
        // This event handler is where the actual work is done.  
        // This method runs on the background thread.  
  
        // Get the BackgroundWorker object that raised this event.  
        System.ComponentModel.BackgroundWorker worker;  
        worker = (System.ComponentModel.BackgroundWorker)sender;  
  
        // Get the Words object and call the main method.  
        Words WC = (Words)e.Argument;  
        WC.CountWords(worker, e);  
    }  
  
    private void StartThread()  
    {  
        // This method runs on the main thread.  
        this.WordsCounted.Text = "0";  
  
        // Initialize the object that the background worker calls.  
        Words WC = new Words();  
        WC.CompareString = this.CompareString.Text;  
        WC.SourceFile = this.SourceFile.Text;  
  
        // Start the asynchronous operation.  
        backgroundWorker1.RunWorkerAsync(WC);  
    }  
    ```  
  
2.  通过窗体上的 `Start` 按钮调用 `StartThread` 方法：  
  
    ```csharp  
    private void Start_Click(object sender, EventArgs e)  
    {  
        StartThread();  
    }  
    ```  
  
    ##### <a name="to-implement-a-cancel-button-that-stops-the-thread"></a>实现停止线程的“取消”按钮  
  
    -   从 `Cancel` 按钮的 `Click` 事件处理程序中调用 `StopThread` 过程。  
  
        ```csharp  
        private void Cancel_Click(object sender, EventArgs e)  
        {  
            // Cancel the asynchronous operation.  
            this.backgroundWorker1.CancelAsync();  
        }  
        ```  
  
## <a name="testing"></a>测试  
 现在可以测试应用程序以确保其正常运行。  
  
#### <a name="to-test-the-application"></a>测试应用程序  
  
1.  按 F5 运行该应用程序。  
  
2.  显示窗体时，在 `sourceFile` 框中输入想测试的文件的文件路径。 例如，假设测试文件的名称为 Test.txt，则输入 C:\Test.txt。  
  
3.  在第二个文本框中，输入要让该应用程序在文本文件中搜索的字词或短语。  
  
4.  单击 `Start` 按钮。 `LinesCounted` 按钮应立即开始递增。 完成后，应用程序将显示“计数完成”消息。  
  
#### <a name="to-test-the-cancel-button"></a>测试“取消”按钮  
  
1.  按 F5 启动该应用程序，按照前面过程所述输入文件名和搜索字词。 请确保所选择的文件足够大，以确保在搜索结束之前有时间取消该过程。  
  
2.  单击 `Start` 按钮启动应用程序。  
  
3.  单击 `Cancel` 按钮。 应用程序应立即停止计数。  
  
## <a name="next-steps"></a>后续步骤  
 此应用程序包含一些基本错误处理。 它可检测空白搜索字符串。 可以通过处理其他错误（如超过可以计数的最大字词数或行数）使该程序更加可靠。  
  
## <a name="see-also"></a>请参阅  
 [线程处理 (C#)](../../../../csharp/programming-guide/concepts/threading/index.md)   
 [如何：订阅和取消订阅事件](../../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)

