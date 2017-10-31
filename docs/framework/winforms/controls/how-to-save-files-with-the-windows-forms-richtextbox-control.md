---
title: "如何：在 Windows 窗体 RichTextBox 控件中保存文件 | Microsoft Docs"
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
  - ".rtf 文件, 在 RichTextBox 控件中保存"
  - "示例 [Windows 窗体], 文本框"
  - "文件, 用 RichTextBox 控件保存"
  - "RichTextBox 控件 [Windows 窗体], 保存文件"
  - "RTF 文件, 在 RichTextBox 控件中保存"
  - "保存文件"
  - "保存文件, RichTextBox 控件"
  - "文本文件, 从 RichTextBox 控件中保存"
ms.assetid: 4a58ec19-84d1-4383-9110-298c06adcfca
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：在 Windows 窗体 RichTextBox 控件中保存文件
Windows 窗体 <xref:System.Windows.Forms.RichTextBox> 控件可以用下面几种格式之一写入它显示的信息：  
  
-   纯文本  
  
-   Unicode 纯文本  
  
-   RTF 格式  
  
-   用空格取代 OLE 对象的 RTF  
  
-   带有 OLE 对象的文本化表示形式的纯文本  
  
 若要保存文件，请调用 <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> 方法。  也可以使用 **SaveFile** 方法将数据保存到流中。  有关更多信息，请参见 <xref:System.Windows.Forms.RichTextBox.SaveFile%28System.IO.Stream%2CSystem.Windows.Forms.RichTextBoxStreamType%29>。  
  
### 将控件的内容保存到文件  
  
1.  确定要保存的文件的路径。  
  
     若要在实际应用程序中实现此操作，通常可使用 <xref:System.Windows.Forms.SaveFileDialog> 组件。  有关概述，请参见[SaveFileDialog 组件概述](../../../../docs/framework/winforms/controls/savefiledialog-component-overview-windows-forms.md)。  
  
2.  调用 <xref:System.Windows.Forms.RichTextBox> 控件的 <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> 方法，指定要保存的文件以及可选文件类型。  如果调用该方法时仅使用文件名作为其唯一参数，则该文件将保存为 RTF 文件。  若要指定其他文件类型，请以 <xref:System.Windows.Forms.RichTextBoxStreamType> 枚举的值作为其第二个参数来调用该方法。  
  
     在下面的示例中，RTF 文件位置的路径设置为**“我的文档”**文件夹。  使用此位置是因为可假定大多数运行 Windows 操作系统的计算机都包含该文件夹。  选择此位置还允许具有最低系统访问级别的用户安全地运行应用程序。  下面的示例假定一个已添加了 <xref:System.Windows.Forms.RichTextBox> 控件的窗体。  
  
    ```vb  
    Public Sub SaveFile()  
       ' You should replace the bold file name in the   
       ' sample below with a file name of your own choosing.  
       RichTextBox1.SaveFile(System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Testdoc.rtf", _  
          RichTextBoxStreamType.RichNoOleObjs)  
    End Sub  
  
    ```  
  
    ```csharp  
    public void SaveFile()  
    {  
       // You should replace the bold file name in the   
       // sample below with a file name of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       richTextBox1.SaveFile(System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Testdoc.rtf",  
          RichTextBoxStreamType.RichNoOleObjs);  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void SaveFile()  
       {  
          // You should replace the bold file name in the   
          // sample below with a file name of your own choosing.  
          richTextBox1->SaveFile(String::Concat  
             (System::Environment::GetFolderPath  
             (System::Environment::SpecialFolder::Personal),  
             "\\Testdoc.rtf"), RichTextBoxStreamType::RichNoOleObjs);  
       }  
    ```  
  
    > [!IMPORTANT]
    >  本示例创建新的文件（如果该文件尚未存在）。  如果应用程序需要创建文件，则应用程序需要文件夹的“创建”访问权限。  权限是使用访问控制列表设置的。  如果该文件已经存在，则应用程序仅需要“写入”访问权限（它是一个权限较弱的特权）。  应尽可能在部署过程中创建文件并仅授予单个文件的“读取”访问权限，而不是授予文件夹的“创建”访问权限，这样做更安全。  而且，更为安全的方法是将数据写入用户文件夹，而不是写入根文件夹或“Program Files”文件夹。  
  
## 请参阅  
 <xref:System.Windows.Forms.RichTextBox.SaveFile%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.RichTextBox>   
 [RichTextBox 控件](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)