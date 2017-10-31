---
title: "如何：使用 Windows 窗体 FolderBrowserDialog 组件选择文件夹 | Microsoft Docs"
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
  - "目录 [Windows 窗体], 选择"
  - "目录 [Windows 窗体], 选择"
  - "FolderBrowserDialog 组件 [Windows 窗体], 选择目录"
  - "文件夹 [Windows 窗体], 选择"
  - "文件夹 [Windows 窗体], 选择"
ms.assetid: 4593670e-7c7d-4661-b46b-4ffb63258adb
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用 Windows 窗体 FolderBrowserDialog 组件选择文件夹
通常，在您创建的 Windows 应用程序内，您需要提示用户选择文件夹，最常见的目的是为了保存一组文件。  Windows 窗体 <xref:System.Windows.Forms.FolderBrowserDialog> 组件使您能够轻松地完成此任务。  
  
### 使用 FolderBrowserDialog 组件选择文件夹  
  
1.  在过程中检查 <xref:System.Windows.Forms.FolderBrowserDialog> 组件的 <xref:System.Windows.Forms.Form.DialogResult%2A> 属性，以查看该对话框是如何关闭的并获取 <xref:System.Windows.Forms.FolderBrowserDialog> 组件的 <xref:System.Windows.Forms.FolderBrowserDialog.SelectedPath%2A> 属性值。  
  
2.  如果您需要设置将出现在对话框树视图中的顶层文件夹，请设置 <xref:System.Windows.Forms.FolderBrowserDialog.RootFolder%2A> 属性，该属性采用 [SpecialFolder](frlrfSystemEnvironmentSpecialFolderClassTopic) 枚举的成员。  
  
3.  另外，您还可以设置 <xref:System.Windows.Forms.FolderBrowserDialog.Description%2A> 属性，该属性指定出现在文件夹浏览器树视图顶部的文本字符串。  
  
     在下面的示例中，<xref:System.Windows.Forms.FolderBrowserDialog> 组件用于选择文件夹，这类似于在 Visual Studio 中创建项目时提示选择保存它的文件夹。  在本示例中，文件夹名称随后显示在窗体上的 <xref:System.Windows.Forms.TextBox> 控件中。  将文件夹名称置于可编辑区域（例如 <xref:System.Windows.Forms.TextBox> 控件）中是个好主意，这样，用户就可在出现错误或其他问题时编辑他们的选择。  本示例假定窗体具有一个 <xref:System.Windows.Forms.FolderBrowserDialog> 组件和一个 <xref:System.Windows.Forms.TextBox> 控件。  
  
    ```vb  
    Public Sub ChooseFolder()  
        If FolderBrowserDialog1.ShowDialog() = DialogResult.OK Then  
            TextBox1.Text = FolderBrowserDialog1.SelectedPath  
        End If  
    End Sub  
  
    ```  
  
    ```csharp  
    public void ChooseFolder()  
    {  
        if (folderBrowserDialog1.ShowDialog() == DialogResult.OK)   
        {  
            textBox1.Text = folderBrowserDialog1.SelectedPath;  
        }  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void ChooseFolder()  
       {  
          if (folderBrowserDialog1->ShowDialog() == DialogResult::OK)  
          {  
             textBox1->Text = folderBrowserDialog1->SelectedPath;  
          }  
       }  
    ```  
  
    > [!IMPORTANT]
    >  若要使用此类，程序集要求具有由 [FileIOPermissionAttribute.PathDiscoveryProperty](frlrfSystemSecurityPermissionsFileIOPermissionAttributeClassPathDiscoveryTopic) 属性（<xref:System.Security.Permissions.FileIOPermissionAccess> 枚举的一部分）授予的特权级别。  如果在部分信任的上下文中运行，该过程可能会引发异常，因为没有足够的特权。  有关更多信息，请参见 [代码访问安全性基础知识](../../../../docs/framework/misc/code-access-security-basics.md)。  
  
 有关如何保存文件的更多信息，请参见 [如何：使用 SaveFileDialog 组件保存文件](../../../../docs/framework/winforms/controls/how-to-save-files-using-the-savefiledialog-component.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.FolderBrowserDialog>   
 [FolderBrowserDialog 组件概述（Windows 窗体）](../../../../docs/framework/winforms/controls/folderbrowserdialog-component-overview-windows-forms.md)   
 [FolderBrowserDialog 组件](../../../../docs/framework/winforms/controls/folderbrowserdialog-component-windows-forms.md)