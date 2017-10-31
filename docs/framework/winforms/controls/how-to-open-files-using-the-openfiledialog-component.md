---
title: "如何：使用 OpenFileDialog 组件打开文件 | Microsoft Docs"
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
  - "文件, 使用 OpenFileDialog 组件打开"
  - "OpenFile 方法"
  - "OpenFile 方法, OpenFileDialog 组件"
  - "OpenFileDialog 组件, 打开文件"
ms.assetid: 9d88367a-cc21-4ffd-be74-89fd63767d35
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：使用 OpenFileDialog 组件打开文件
用户可以使用 <xref:System.Windows.Forms.OpenFileDialog> 组件浏览他们的计算机以及网络中任何计算机上的文件夹，并选择打开一个或多个文件。  该对话框返回用户在对话框中选定的文件的路径和名称。  
  
 用户选定要打开的文件后，可以使用两种机制来打开文件。  如果希望使用文件流，则可以创建 <xref:System.IO.StreamReader> 类的实例。  另一种方法是使用 <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> 方法打开选定的文件。  
  
 下面的第一个示例包括 <xref:System.Security.Permissions.FileIOPermission> 权限检查（如下面的“安全说明”中所述），但示例授予了您访问文件名的权限。  您可以在本地计算机、Intranet 以及 Internet 区域中使用这种技术。  第二个方法也执行了 <xref:System.Security.Permissions.FileIOPermission> 权限检查，但更适合于 Intranet 或 Internet 区域中的应用程序。  
  
### 使用 OpenFileDialog 组件以流方式打开文件  
  
1.  显示**“打开文件”**对话框，并调用方法打开用户选定的文件。  
  
     其中一个方法是使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法显示“打开文件”对话框，并使用 <xref:System.IO.StreamReader> 类的实例打开文件。  
  
     下面的示例使用 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件处理程序打开 <xref:System.Windows.Forms.OpenFileDialog> 组件的实例。  当用户选定某个文件并单击**“确定”**后，将打开对话框中选定的文件。  在这种情况下，内容将显示在一个消息框中，并且只是说明已读取文件流。  
  
    > [!IMPORTANT]
    >  若要获取或设置 <xref:System.Windows.Forms.FileDialog.FileName%2A> 属性，程序集需要具有由 <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName> 类授予的特权级别。  如果在部分信任的上下文中运行，则该进程可能会因特权不足而引发一个异常。  有关更多信息，请参见[代码访问安全性基础知识](../../../../docs/framework/misc/code-access-security-basics.md)。  
  
     本示例假设窗体具有一个 <xref:System.Windows.Forms.Button> 控件和一个 <xref:System.Windows.Forms.OpenFileDialog> 组件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       If OpenFileDialog1.ShowDialog() = System.Windows.Forms.DialogResult.OK Then  
         Dim sr As New System.IO.StreamReader(OpenFileDialog1.FileName)  
         MessageBox.Show(sr.ReadToEnd)  
         sr.Close()  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(openFileDialog1.ShowDialog() == System.Windows.Forms.DialogResult.OK)  
       {  
          System.IO.StreamReader sr = new   
             System.IO.StreamReader(openFileDialog1.FileName);  
          MessageBox.Show(sr.ReadToEnd());  
          sr.Close();  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if(openFileDialog1->ShowDialog() == System::Windows::Forms::DialogResult::OK)  
          {  
             System::IO::StreamReader ^ sr = gcnew  
                System::IO::StreamReader(openFileDialog1->FileName);  
             MessageBox::Show(sr->ReadToEnd());  
             sr->Close();  
          }  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码来注册事件处理程序。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
    > [!NOTE]
    >  有关从文件流中进行读取的更多信息，请参见 [FileStream.BeginRead 方法](frlrfSystemIOFileStreamClassBeginReadTopic)和 [FileStream.Read 方法](https://msdn.microsoft.com/en-us/library/system.io.filestream.read.aspx)。  
  
### 使用 OpenFileDialog 组件以文件方式打开文件  
  
1.  使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法显示对话框，并使用 <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> 方法打开文件。  
  
     <xref:System.Windows.Forms.OpenFileDialog> 组件的 <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> 方法返回构成文件的字节。  这些字节为您提供了一个可从中读取的流。  在下面的示例中，将实例化一个具有“cursor”筛选器的 <xref:System.Windows.Forms.OpenFileDialog> 组件，使用户只能选择具有`.cur` 文件扩展名的文件。  如果选择了一个`.cur` 文件，该窗体的光标将设置为选定的光标。  
  
    > [!IMPORTANT]
    >  若要调用 <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> 方法，程序集需要具有由 <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName> 类授予的特权级别。  如果在部分信任的上下文中运行，则该进程可能会因特权不足而引发一个异常。  有关更多信息，请参见[代码访问安全性基础知识](../../../../docs/framework/misc/code-access-security-basics.md)。  
  
     本示例假设窗体具有一个 <xref:System.Windows.Forms.Button> 控件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       ' Displays an OpenFileDialog so the user can select a Cursor.  
       Dim openFileDialog1 As New OpenFileDialog()  
       openFileDialog1.Filter = "Cursor Files|*.cur"  
       openFileDialog1.Title = "Select a Cursor File"  
  
       ' Show the Dialog.  
       ' If the user clicked OK in the dialog and   
       ' a .CUR file was selected, open it.  
       If openFileDialog1.ShowDialog() = System.Windows.Forms.DialogResult.OK Then  
         ' Assign the cursor in the Stream to the Form's Cursor property.  
         Me.Cursor = New Cursor(openFileDialog1.OpenFile())  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // Displays an OpenFileDialog so the user can select a Cursor.  
       OpenFileDialog openFileDialog1 = new OpenFileDialog();  
       openFileDialog1.Filter = "Cursor Files|*.cur";  
       openFileDialog1.Title = "Select a Cursor File";  
  
       // Show the Dialog.  
       // If the user clicked OK in the dialog and  
       // a .CUR file was selected, open it.  
        if (openFileDialog1.ShowDialog() == System.Windows.Forms.DialogResult.OK)  
       {  
          // Assign the cursor in the Stream to the Form's Cursor property.  
          this.Cursor = new Cursor(openFileDialog1.OpenFile());  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // Displays an OpenFileDialog so the user can select a Cursor.  
          OpenFileDialog ^ openFileDialog1 = new OpenFileDialog();  
          openFileDialog1->Filter = "Cursor Files|*.cur";  
          openFileDialog1->Title = "Select a Cursor File";  
  
          // Show the Dialog.  
          // If the user clicked OK in the dialog and  
          // a .CUR file was selected, open it.  
          if (openFileDialog1->ShowDialog() == System::Windows::Forms::DialogResult::OK)  
          {  
             // Assign the cursor in the Stream to  
             // the Form's Cursor property.  
             this->Cursor = gcnew  
                System::Windows::Forms::Cursor(  
                openFileDialog1->OpenFile());  
          }  
       }  
  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码来注册事件处理程序。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.OpenFileDialog>   
 [OpenFileDialog 组件](../../../../docs/framework/winforms/controls/openfiledialog-component-windows-forms.md)