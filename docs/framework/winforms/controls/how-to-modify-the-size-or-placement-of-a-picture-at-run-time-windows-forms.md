---
title: "如何：在运行时修改图片的大小或位置（Windows 窗体） | Microsoft Docs"
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
  - "示例 [Windows 窗体], PictureBox 控件"
  - "图像 [Windows 窗体], 控制 PictureBox 控件中的放置操作 [Windows 窗体]"
  - "PictureBox 控件 [Windows 窗体], 图片大小和对齐方式"
  - "pictures, 控制 PictureBox 控件中的放置操作 [Windows 窗体]"
ms.assetid: d0b332a3-fae2-4891-957c-dc3e17743326
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在运行时修改图片的大小或位置（Windows 窗体）
如果您在窗体上使用 Windows 窗体 <xref:System.Windows.Forms.PictureBox> 控件，则可将其 <xref:System.Windows.Forms.PictureBox.SizeMode%2A> 属性设置为：  
  
-   将图片的左上角与控件的左上角对齐  
  
-   使图片在控件内居中  
  
-   调整控件的大小以适合其显示的图片  
  
-   拉伸所显示的任何图片以适合控件  
  
 拉伸图片（尤其是位图格式的图片）可能导致图像质量受损。  图元文件（运行时绘制图像的图形指令列表）比位图更适合于拉伸图片。  
  
### 在运行时设置 SizeMode 属性  
  
1.  将 <xref:System.Windows.Forms.PictureBox.SizeMode%2A> 设置为 <xref:System.Windows.Forms.PictureBoxSizeMode>（默认值）、<xref:System.Windows.Forms.PictureBoxSizeMode>、<xref:System.Windows.Forms.PictureBoxSizeMode> 或 <xref:System.Windows.Forms.PictureBoxSizeMode>。  <xref:System.Windows.Forms.PictureBoxSizeMode> 表示将图像放置在控件的左上角；如果图像比控件大，则会对其下边缘和右边缘进行剪裁。  <xref:System.Windows.Forms.PictureBoxSizeMode> 表示图像将在控件中居中放置；如果图像比控件大，则会对图像超出控件的边缘进行剪裁。  <xref:System.Windows.Forms.PictureBoxSizeMode> 表示将控件的大小调整为图像的大小。  <xref:System.Windows.Forms.PictureBoxSizeMode> 则与之相反，它表示将图像的大小调整为控件的大小。  
  
     在下面的示例中，图像位置的路径设置是 My Documents 文件夹。  这样做是因为可假定大多数运行 Windows 操作系统的计算机都包含此目录。  这还将允许具有最低系统访问级别的用户安全地运行应用程序。  下面的示例假定一个已添加了 <xref:System.Windows.Forms.PictureBox> 控件的窗体。  
  
    ```vb  
    Private Sub StretchPic()  
       ' Stretch the picture to fit the control.  
       PictureBox1.SizeMode = PictureBoxSizeMode.StretchImage  
       ' Load the picture into the control.  
       ' You should replace the bold image   
       ' in the sample below with an icon of your own choosing.  
       PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void StretchPic(){  
       // Stretch the picture to fit the control.  
       PictureBox1.SizeMode = PictureBoxSizeMode.StretchImage;  
       // Load the picture into the control.  
       // You should replace the bold image   
       // in the sample below with an icon of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       + @"\Image.gif")  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void StretchPic()  
       {  
          // Stretch the picture to fit the control.  
          pictureBox1->SizeMode = PictureBoxSizeMode::StretchImage;  
          // Load the picture into the control.  
          // You should replace the bold image   
          // in the sample below with an icon of your own choosing.  
          pictureBox1->Image = Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.PictureBox>   
 [如何：使用设计器加载图片](../../../../docs/framework/winforms/controls/how-to-load-a-picture-using-the-designer-windows-forms.md)   
 [PictureBox 控件概述](../../../../docs/framework/winforms/controls/picturebox-control-overview-windows-forms.md)   
 [如何：在运行时设置图片](../../../../docs/framework/winforms/controls/how-to-set-pictures-at-run-time-windows-forms.md)   
 [PictureBox 控件](../../../../docs/framework/winforms/controls/picturebox-control-windows-forms.md)