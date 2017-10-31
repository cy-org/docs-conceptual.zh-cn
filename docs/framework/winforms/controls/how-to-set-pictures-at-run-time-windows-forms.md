---
title: "如何：在运行时设置图片（Windows 窗体） | Microsoft Docs"
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
  - "位图 [Windows 窗体], 在 PictureBox 控件中显示 [Windows 窗体]"
  - "示例 [Windows 窗体], PictureBox 控件"
  - "图像 [Windows 窗体], 使用 PictureBox 控件添加 [Windows 窗体]"
  - "PictureBox 控件 [Windows 窗体], 添加图像"
  - "PictureBox 控件 [Windows 窗体], 添加图片"
  - "pictures, 设置显示"
ms.assetid: 18ca41d0-68a5-4660-985e-a6c1fbc01d76
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：在运行时设置图片（Windows 窗体）
可通过编程方式设置 Windows 窗体 <xref:System.Windows.Forms.PictureBox> 控件显示的图像。  
  
### 以编程方式设置图片  
  
-   使用 <xref:System.Drawing.Image> 类的 <xref:System.Drawing.Image.FromFile%2A> 方法设置 <xref:System.Windows.Forms.PictureBox.Image%2A> 属性。  
  
     在下面的示例中，图像位置的路径设置是 My Documents 文件夹。  这样做是因为可假定大多数运行 Windows 操作系统的计算机都包含此目录。  这还将允许具有最低系统访问级别的用户安全地运行应用程序。  下面的示例假定一个已添加了 <xref:System.Windows.Forms.PictureBox> 控件的窗体。  
  
    ```vb  
    Private Sub LoadNewPict()  
       ' You should replace the bold image   
       ' in the sample below with an icon of your own choosing.  
       PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void LoadNewPict(){  
       // You should replace the bold image   
       // in the sample below with an icon of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       pictureBox1.Image = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void LoadNewPict()  
       {  
          // You should replace the bold image   
          // in the sample below with an icon of your own choosing.  
          pictureBox1->Image = Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
       }  
    ```  
  
### 清除图形  
  
-   首先，释放图像正使用的内存，然后清除图形。  如果内存管理成为问题所在，则垃圾回收稍后会释放内存。  
  
    ```vb  
    If Not (PictureBox1.Image Is Nothing) Then  
       PictureBox1.Image.Dispose()  
       PictureBox1.Image = Nothing  
    End If  
  
    ```  
  
    ```csharp  
    if (pictureBox1.Image != null)   
    {  
       pictureBox1.Image.Dispose();  
       pictureBox1.Image = null;  
    }  
  
    ```  
  
    ```cpp  
    if (pictureBox1->Image != nullptr)  
    {  
       pictureBox1->Image->Dispose();  
       pictureBox1->Image = nullptr;  
    }  
    ```  
  
    > [!NOTE]
    >  有关为何以这种方式使用 <xref:System.Drawing.Image.Dispose%2A> 方法的更多信息，请参见 [Cleaning Up Unmanaged Resources](../../../../docs/standard/garbage-collection/unmanaged.md)。  
  
     即使图形是在设计时加载到控件中的，此代码也将清除图像。  
  
## 请参阅  
 <xref:System.Windows.Forms.PictureBox>   
 <xref:System.Drawing.Image.FromFile%2A?displayProperty=fullName>   
 [PictureBox 控件概述](../../../../docs/framework/winforms/controls/picturebox-control-overview-windows-forms.md)   
 [如何：使用设计器加载图片](../../../../docs/framework/winforms/controls/how-to-load-a-picture-using-the-designer-windows-forms.md)   
 [如何：在运行时修改图片的大小或位置](../../../../docs/framework/winforms/controls/how-to-modify-the-size-or-placement-of-a-picture-at-run-time-windows-forms.md)   
 [PictureBox 控件](../../../../docs/framework/winforms/controls/picturebox-control-windows-forms.md)