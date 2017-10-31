---
title: "如何：设置 Windows 窗体 ProgressBar 控件显示的值 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Increment 方法"
  - "PerformStep 方法"
  - "进度控件, 显示的设置值"
  - "ProgressBar 控件 [Windows 窗体], 显示的设置值"
  - "Step 属性"
  - "Value 属性"
ms.assetid: 0e5010ad-1e9a-4271-895e-5a3d24d37a26
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：设置 Windows 窗体 ProgressBar 控件显示的值
> [!IMPORTANT]
>  <xref:System.Windows.Forms.ToolStripProgressBar> 控件取代了 <xref:System.Windows.Forms.ProgressBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ProgressBar> 控件以实现向后兼容并供将来使用。  
  
 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 使您可以通过几种不同的方法显示 <xref:System.Windows.Forms.ProgressBar> 控件中的给定值。  选择的方法将取决于您所要执行的任务或要解决的问题。  下表说明了可以选择的方法。  
  
|方法|说明|  
|--------|--------|  
|直接设置 <xref:System.Windows.Forms.ProgressBar> 控件的值。|如果您知道任务中涉及的测量项总数，此方法非常有用，例如从数据源中读取记录。  此外，如果您只需要设置该值一次或两次，这将是实现该目的的简便方法。  最后，如果您需要减小进度栏显示的值，请使用此方法。|  
|使 <xref:System.Windows.Forms.ProgressBar> 的显示值按固定值递增。|如果需要显示最小值和最大值之间的简单计数，此方法非常有用，例如运行时间或已知文件总数中已处理的文件数。|  
|使 <xref:System.Windows.Forms.ProgressBar> 的显示值按可变值递增。|如果需要多次以不同数量更改显示值，此方法非常有用。  例如，显示将一系列文件写入磁盘时所占用的硬盘空间量。|  
  
 设置进度栏的显示值的最直接方式是设置 <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性。  该操作可以在设计时或运行时进行。  
  
### 直接设置 ProgressBar 值  
  
1.  设置 <xref:System.Windows.Forms.ProgressBar> 控件的 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 和 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 值。  
  
2.  在代码中，将该控件的 <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性设置为已设定的最小值与最大值之间的一个整数值。  
  
    > [!NOTE]
    >  如果将 <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性设置为 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 和 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 属性设定的边界之外的值，该控件将引发 <xref:System.ArgumentException> 异常。  
  
     下面的代码示例说明如何直接设置 <xref:System.Windows.Forms.ProgressBar> 值。  该代码从数据源中读取记录，并在每次读取数据记录时更新进度栏和标签。  该示例要求窗体有一个 <xref:System.Windows.Forms.Label> 控件、一个 <xref:System.Windows.Forms.ProgressBar> 控件以及一个数据表，该数据表中名为`CustomerRow` 的行具有`FirstName` 和`Last Name` 字段。  
  
    ```vb  
    Public Sub CreateNewRecords()  
       ' Sets the progress bar's Maximum property to  
       ' the total number of records to be created.  
       ProgressBar1.Maximum = 20  
  
       ' Creates a new record in the dataset.  
       ' NOTE: The code below will not compile, it merely  
       ' illustrates how the progress bar would be used.  
       Dim anyRow As CustomerRow = DatasetName.ExistingTable.NewRow  
       anyRow.FirstName = "Stephen"  
       anyRow.LastName = "James"  
       ExistingTable.Rows.Add(anyRow)  
  
       ' Increases the value displayed by the progress bar.  
       ProgressBar1.Value += 1  
       ' Updates the label to show that a record was read.  
       Label1.Text = "Records Read = " & ProgressBar1.Value.ToString()  
    End Sub  
  
    ```  
  
    ```csharp  
    public void createNewRecords()  
    {  
       // Sets the progress bar's Maximum property to  
       // the total number of records to be created.  
       progressBar1.Maximum = 20;  
  
       // Creates a new record in the dataset.  
       // NOTE: The code below will not compile, it merely  
       // illustrates how the progress bar would be used.  
       CustomerRow anyRow = DatasetName.ExistingTable.NewRow();  
       anyRow.FirstName = "Stephen";  
       anyRow.LastName = "James";  
       ExistingTable.Rows.Add(anyRow);  
  
       // Increases the value displayed by the progress bar.  
       progressBar1.Value += 1;  
       // Updates the label to show that a record was read.  
       label1.Text = "Records Read = " + progressBar1.Value.ToString();  
    }  
    ```  
  
     如果要显示按固定时间间隔增长的进度，则可以设置该值，然后调用方法，使 <xref:System.Windows.Forms.ProgressBar> 控件的值按该时间间隔递增。  对于计时器以及其他一些您无法以整体的百分比测量进度的方案，这是非常有用的。  
  
### 使进度栏按固定值递增  
  
1.  设置 <xref:System.Windows.Forms.ProgressBar> 控件的 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 和 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 值。  
  
2.  将控件的 <xref:System.Windows.Forms.ProgressBar.Step%2A> 属性设置为一个整数，该整数代表进度栏的显示值递增的数量。  
  
3.  调用 <xref:System.Windows.Forms.ProgressBar.PerformStep%2A> 方法，使显示值按 <xref:System.Windows.Forms.ProgressBar.Step%2A> 属性中设置的数量进行更改。  
  
     下面的代码示例说明进度栏如何维护复制操作中的文件计数。  
  
     在下面的示例中，当每个文件读入内存时，进度栏和标签都会相应地更新，以反映读取的文件总数。  该示例要求窗体有一个 <xref:System.Windows.Forms.Label> 控件和一个 <xref:System.Windows.Forms.ProgressBar> 控件。  
  
    ```vb  
    Public Sub LoadFiles()  
       ' Sets the progress bar's minimum value to a number representing  
       ' no operations complete -- in this case, no files read.  
       ProgressBar1.Minimum = 0  
       ' Sets the progress bar's maximum value to a number representing  
       ' all operations complete -- in this case, all five files read.  
       ProgressBar1.Maximum = 5  
       ' Sets the Step property to amount to increase with each iteration.  
       ' In this case, it will increase by one with every file read.  
       ProgressBar1.Step = 1  
  
       ' Dimensions a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be copied into memory,  
       ' so the loop will execute 5 times.  
       For i = 0 To 4  
          ' Insert code to copy a file  
          ProgressBar1.PerformStep()  
          ' Update the label to show that a file was read.  
          Label1.Text = "# of Files Read = " & ProgressBar1.Value.ToString  
       Next i  
    End Sub  
  
    ```  
  
    ```csharp  
    public void loadFiles()  
    {  
       // Sets the progress bar's minimum value to a number representing  
       // no operations complete -- in this case, no files read.  
       progressBar1.Minimum = 0;  
       // Sets the progress bar's maximum value to a number representing  
       // all operations complete -- in this case, all five files read.  
       progressBar1.Maximum = 5;  
       // Sets the Step property to amount to increase with each iteration.  
       // In this case, it will increase by one with every file read.  
       progressBar1.Step = 1;  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be copied into memory,  
       // so the loop will execute 5 times.  
       for (int i = 0; i <= 4; i++)  
       {  
          // Inserts code to copy a file  
          progressBar1.PerformStep();  
          // Updates the label to show that a file was read.  
          label1.Text = "# of Files Read = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
     最后，可以使进度栏的显示值每次递增的数量都是唯一的。  这在您记录一系列唯一的操作时非常有用，例如将不同大小的文件写入硬盘，或者按整体的百分比测量进度。  
  
### 使进度栏按动态值递增  
  
1.  设置 <xref:System.Windows.Forms.ProgressBar> 控件的 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 和 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 值。  
  
2.  调用 <xref:System.Windows.Forms.ProgressBar.Increment%2A> 方法，使显示值按指定的整数进行更改。  
  
     下面的代码示例说明在复制操作期间，进度栏如何计算已使用的磁盘空间量。  
  
     在下面的示例中，当每个文件写入硬盘时，进度栏和标签都会相应地更新，以反映可用的硬盘空间量。  该示例要求窗体有一个 <xref:System.Windows.Forms.Label> 控件和一个 <xref:System.Windows.Forms.ProgressBar> 控件。  
  
    ```vb  
    Public Sub ReadFiles()  
       ' Sets the progress bar's minimum value to a number   
       ' representing the hard disk space before the files are read in.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example and  
       ' will not compile.  
       ProgressBar1.Minimum = AvailableDiskSpace()  
       ' Sets the progress bar's maximum value to a number   
       ' representing the total hard disk space.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example   
       ' and will not compile.  
       ProgressBar1.Maximum = TotalDiskSpace()  
  
       ' Dimension a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be written to the disk,  
       ' so it will execute the loop 5 times.  
       For i = 1 To 5  
          ' Insert code to read a file into memory and update file size.  
          ' Increases the progress bar's value based on the size of   
          ' the file currently being written.  
          ProgressBar1.Increment(FileSize)  
          ' Updates the label to show available drive space.  
          Label1.Text = "Current Disk Space Used = " &_   
          ProgressBar1.Value.ToString()  
       Next i  
    End Sub  
  
    ```  
  
    ```csharp  
    public void readFiles()  
    {  
       // Sets the progress bar's minimum value to a number   
       // representing the hard disk space before the files are read in.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example and   
       // will not compile.  
       progressBar1.Minimum = AvailableDiskSpace();  
       // Sets the progress bar's maximum value to a number   
       // representing the total hard disk space.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example   
       // and will not compile.  
       progressBar1.Maximum = TotalDiskSpace();  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be written  
       // to the disk, so it will execute the loop 5 times.  
       for (int i = 1; i<= 5; i++)  
       {  
          // Insert code to read a file into memory and update file size.  
          // Increases the progress bar's value based on the size of   
          // the file currently being written.  
          progressBar1.Increment(FileSize);  
          // Updates the label to show available drive space.  
          label1.Text = "Current Disk Space Used = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ProgressBar>   
 <xref:System.Windows.Forms.ToolStripProgressBar>   
 [ProgressBar 控件概述](../../../../docs/framework/winforms/controls/progressbar-control-overview-windows-forms.md)   
 [ProgressBar 控件](../../../../docs/framework/winforms/controls/progressbar-control-windows-forms.md)