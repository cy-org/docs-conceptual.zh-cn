---
title: "如何：使用 SaveFileDialog 组件保存文件 | Microsoft Docs"
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
  - "文件, 保存"
  - "OpenFile 方法, 使用 SaveFileDialog 组件保存文件"
  - "SaveFileDialog 组件, 保存文件"
  - "保存文件"
ms.assetid: 02e8f409-b83f-4707-babb-e71f6b223d90
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：使用 SaveFileDialog 组件保存文件
用户可以使用 <xref:System.Windows.Forms.SaveFileDialog> 组件浏览文件系统并选择要保存的文件。  该对话框返回用户在对话框中选定的文件的路径和名称。  不过，您必须编写代码才能真正地将文件写入磁盘。  
  
### 使用 SaveFileDialog 组件保存文件  
  
-   显示**“保存文件”**对话框并调用一个方法保存用户选定的文件。  
  
     使用 <xref:System.Windows.Forms.SaveFileDialog> 组件的 <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A> 方法保存文件。  此方法提供了一个可以写入的 <xref:System.IO.Stream> 对象。  
  
     下面的示例使用 <xref:System.Windows.Forms.DialogResult> 属性获取文件的名称，并使用 <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> 方法保存文件。  <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A> 方法提供了可以写入文件的流。  
  
     在下面的示例中，有一个分配了图像的 <xref:System.Windows.Forms.Button> 控件。  单击该按钮时，将使用一个允许 .gif、.jpeg 和 .bmp 类型文件的筛选器实例化 <xref:System.Windows.Forms.SaveFileDialog> 组件。  如果在“保存文件”对话框中选定了此类型的文件，那么将保存按钮的图像。  
  
    > [!IMPORTANT]
    >  若要获取或设置 <xref:System.Windows.Forms.FileDialog.FileName%2A> 属性，程序集需要具有由 <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName> 类授予的特权级别。  如果在部分信任的上下文中运行，则该进程可能会因特权不足而引发一个异常。  有关更多信息，请参见[代码访问安全性基础知识](../../../../docs/framework/misc/code-access-security-basics.md)。  
  
     该示例假设窗体上有一个 <xref:System.Windows.Forms.Button> 控件，该控件的 <xref:System.Windows.Forms.ButtonBase.Image%2A> 属性设置为 .gif、.jpeg 或 .bmp 类型的文件。  
  
    > [!NOTE]
    >  <xref:System.Windows.Forms.FileDialog> 类的 <xref:System.Windows.Forms.FileDialog.FilterIndex%2A> 属性（根据继承的特性，该属性属于 <xref:System.Windows.Forms.SaveFileDialog> 类）使用从 1 开始的索引。  如果您通过编写代码以特定格式保存数据（例如，以纯文本而不是二进制格式保存文件），那么这一点很重要。  以下示例介绍了该属性。  
  
    ```vb  
    Private Sub Button2_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button2.Click  
       ' Displays a SaveFileDialog so the user can save the Image  
       ' assigned to Button2.  
       Dim saveFileDialog1 As New SaveFileDialog()  
       saveFileDialog1.Filter = "JPeg Image|*.jpg|Bitmap Image|*.bmp|Gif Image|*.gif"  
       saveFileDialog1.Title = "Save an Image File"  
       saveFileDialog1.ShowDialog()  
  
       ' If the file name is not an empty string open it for saving.  
       If saveFileDialog1.FileName <> "" Then  
          ' Saves the Image via a FileStream created by the OpenFile method.  
          Dim fs As System.IO.FileStream = Ctype _  
             (saveFileDialog1.OpenFile(), System.IO.FileStream)  
          ' Saves the Image in the appropriate ImageFormat based upon the  
          ' file type selected in the dialog box.  
          ' NOTE that the FilterIndex property is one-based.  
          Select Case saveFileDialog1.FilterIndex  
             Case 1  
                Me.button2.Image.Save(fs, _  
                   System.Drawing.Imaging.ImageFormat.Jpeg)  
  
             Case 2  
                Me.button2.Image.Save(fs, _  
                   System.Drawing.Imaging.ImageFormat.Bmp)  
  
             Case 3  
                Me.button2.Image.Save(fs, _  
                   System.Drawing.Imaging.ImageFormat.Gif)  
           End Select  
  
           fs.Close()  
        End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button2_Click(object sender, System.EventArgs e)  
    {  
       // Displays a SaveFileDialog so the user can save the Image  
       // assigned to Button2.  
       SaveFileDialog saveFileDialog1 = new SaveFileDialog();  
       saveFileDialog1.Filter = "JPeg Image|*.jpg|Bitmap Image|*.bmp|Gif Image|*.gif";  
       saveFileDialog1.Title = "Save an Image File";  
       saveFileDialog1.ShowDialog();  
  
       // If the file name is not an empty string open it for saving.  
       if(saveFileDialog1.FileName != "")  
       {  
          // Saves the Image via a FileStream created by the OpenFile method.  
          System.IO.FileStream fs =   
             (System.IO.FileStream)saveFileDialog1.OpenFile();  
          // Saves the Image in the appropriate ImageFormat based upon the  
          // File type selected in the dialog box.  
          // NOTE that the FilterIndex property is one-based.  
          switch(saveFileDialog1.FilterIndex)  
          {  
             case 1 :   
             this.button2.Image.Save(fs,   
                System.Drawing.Imaging.ImageFormat.Jpeg);  
             break;  
  
             case 2 :   
             this.button2.Image.Save(fs,   
                System.Drawing.Imaging.ImageFormat.Bmp);  
             break;  
  
             case 3 :   
             this.button2.Image.Save(fs,   
                System.Drawing.Imaging.ImageFormat.Gif);  
             break;  
          }  
  
       fs.Close();  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void button2_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // Displays a SaveFileDialog so the user can save the Image  
          // assigned to Button2.  
          SaveFileDialog ^ saveFileDialog1 = new SaveFileDialog();  
          saveFileDialog1->Filter =   
             "JPeg Image|*.jpg|Bitmap Image|*.bmp|Gif Image|*.gif";  
          saveFileDialog1->Title = "Save an Image File";  
          saveFileDialog1->ShowDialog();  
          // If the file name is not an empty string, open it for saving.  
          if(saveFileDialog1->FileName != "")  
          {  
             // Saves the Image through a FileStream created by  
             // the OpenFile method.  
             System::IO::FileStream ^ fs =   
                safe_cast<System::IO::FileStream*>(  
                saveFileDialog1->OpenFile());  
             // Saves the Image in the appropriate ImageFormat based on  
             // the file type selected in the dialog box.  
             // Note that the FilterIndex property is one based.  
             switch(saveFileDialog1->FilterIndex)  
             {  
                case 1 :  
                   this->button2->Image->Save(fs,  
                      System::Drawing::Imaging::ImageFormat::Jpeg);  
                   break;  
                case 2 :  
                   this->button2->Image->Save(fs,   
                      System::Drawing::Imaging::ImageFormat::Bmp);  
                   break;  
                case 3 :  
                   this->button2->Image->Save(fs,   
                      System::Drawing::Imaging::ImageFormat::Gif);  
                   break;  
             }  
          fs->Close();  
          }  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码来注册事件处理程序。  
  
    ```csharp  
    this.button2.Click += new System.EventHandler(this.button2_Click);  
  
    ```  
  
    ```cpp  
    this->button2->Click += gcnew  
       System::EventHandler(this, &Form1::button2_Click);  
    ```  
  
     有关编写文件流的更多信息，请参见 [FileStream.BeginWrite 方法](frlrfSystemIOFileStreamClassBeginWriteTopic)和 [FileStream.Write 方法](https://msdn.microsoft.com/en-us/library/system.io.filestream.write.aspx)。  
  
    > [!NOTE]
    >  某些控件，如 <xref:System.Windows.Forms.RichTextBox> 控件，具有保存文件的能力。  有关更多信息，请参见 MSDN 联机库技术文章 [Essential Code for Windows Forms Dialog Boxes](http://go.microsoft.com/fwlink/?LinkID=102575)（Windows 窗体对话框的基本代码）的“SaveFileDialog Component”（SaveFileDialog 组件）部分。  
  
## 请参阅  
 <xref:System.Windows.Forms.SaveFileDialog>   
 [SaveFileDialog 组件](../../../../docs/framework/winforms/controls/savefiledialog-component-windows-forms.md)