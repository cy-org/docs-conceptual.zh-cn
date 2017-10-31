---
title: "如何：将文件加载到 Windows 窗体 RichTextBox 控件中 | Microsoft Docs"
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
  - "文本框, 显示文件"
  - "示例 [Windows 窗体], 文本框"
  - ".rtf 文件, 在 RichTextBox 控件中打开"
  - "RTF 文件, 在 RichTextBox 控件中打开"
  - "文本文件, 在 RichTextBox 控件中显示"
  - ".rtf 文件, 在 RichTextBox 控件中显示"
  - "RichTextBox 控件 [Windows 窗体], 打开文件"
  - "RTF 文件, 在 RichTextBox 控件中显示"
ms.assetid: c03451be-f285-4428-a71a-c41e002cc919
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：将文件加载到 Windows 窗体 RichTextBox 控件中
Windows 窗体 <xref:System.Windows.Forms.RichTextBox> 控件可以显示纯文本、Unicode 纯文本或 RTF 格式 \(RTF\) 文件。 若要显示这些文件，请调用 <xref:System.Windows.Forms.RichTextBox.LoadFile%2A> 方法。 还可以使用 <xref:System.Windows.Forms.RichTextBox.LoadFile%2A> 方法从流中加载数据。 有关详细信息，请参阅<xref:System.Windows.Forms.RichTextBox.LoadFile%28System.IO.Stream%2CSystem.Windows.Forms.RichTextBoxStreamType%29>。  
  
### 将文件加载到 RichTextBox 控件中  
  
1.  使用 <xref:System.Windows.Forms.OpenFileDialog> 组件确定要打开的文件的路径。 有关概述，请参阅[OpenFileDialog 组件概述](../../../../docs/framework/winforms/controls/openfiledialog-component-overview-windows-forms.md)。  
  
2.  调用 <xref:System.Windows.Forms.RichTextBox> 控件的 <xref:System.Windows.Forms.RichTextBox.LoadFile%2A> 方法，指定要加载的文件，并且可以指定文件类型。 在下面的示例中，要加载的文件来自 <xref:System.Windows.Forms.OpenFileDialog> 组件的 <xref:System.Windows.Forms.FileDialog.FileName%2A> 属性。 如果调用该方法时仅使用文件名作为其唯一参数，则会假定该文件类型为 RTF。 若要指定其他文件类型，请使用 <xref:System.Windows.Forms.RichTextBoxStreamType> 枚举的值作为其第二个参数来调用该方法。  
  
     在下面的示例中，单击按钮时显示 <xref:System.Windows.Forms.OpenFileDialog> 组件。 然后，在 <xref:System.Windows.Forms.RichTextBox> 控件中打开并显示所选文件。 此示例假定窗体包含一个 `btnOpenFile` 按钮。  
  
    ```vb  
    Private Sub btnOpenFile_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles btnOpenFile.Click  
         If OpenFileDialog1.ShowDialog() = DialogResult.OK Then  
           RichTextBox1.LoadFile(OpenFileDialog1.FileName, _  
              RichTextBoxStreamType.RichText)  
          End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void btnOpenFile_Click(object sender, System.EventArgs e)  
    {  
       if(openFileDialog1.ShowDialog() == DialogResult.OK)  
       {  
         richTextBox1.LoadFile(openFileDialog1.FileName, RichTextBoxStreamType.RichText);  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void btnOpenFile_Click(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          if(openFileDialog1->ShowDialog() == DialogResult::OK)  
          {  
             richTextBox1->LoadFile(openFileDialog1->FileName,  
                RichTextBoxStreamType::RichText);  
          }  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)][!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) 将以下代码放在窗体构造函数中以注册事件处理程序。  
  
    ```csharp  
    this.btnOpenFile.Click += new System.EventHandler(this. btnOpenFile_Click);  
  
    ```  
  
    ```cpp  
    this->btnOpenFile->Click += gcnew   
       System::EventHandler(this, &Form1::btnOpenFile_Click);  
    ```  
  
    > [!IMPORTANT]
    >  若要运行此进程，程序集可能需要 <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName> 类授予的特权等级。 如果在部分信任上下文中运行，该进程可能会因特权不足而引发异常。 有关详细信息，请参阅[代码访问安全性基础知识](../../../../docs/framework/misc/code-access-security-basics.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.RichTextBox.LoadFile%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.RichTextBox>   
 [RichTextBox 控件](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)