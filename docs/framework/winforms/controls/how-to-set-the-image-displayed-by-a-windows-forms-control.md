---
title: "如何：设置 Windows 窗体控件所显示的图像 | Microsoft Docs"
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
  - "Button 控件 [Windows 窗体], 图像"
  - "控件 [Windows 窗体], 图像"
  - "示例 [Windows 窗体], 控件"
  - "图像 [Windows 窗体], Windows 窗体控件"
  - "Windows 窗体控件, 图像"
ms.assetid: 9445af8f-4f62-48b0-a3f6-068058964b9f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：设置 Windows 窗体控件所显示的图像
有些 Windows 窗体控件能够显示图像。  这些图像可以是阐明控件用途的图标，例如按钮上表示**“保存”**命令的磁盘图标。  或者，图标还可以是给控件提供您想要的外观和行为的背景图像。  
  
### 设置控件所显示的图像  
  
1.  将控件的 `Image` 或 `BackgroundImage` 属性设置为 <xref:System.Drawing.Image> 类型的对象。  通常您将会使用 <xref:System.Drawing.Image.FromFile%2A> 方法从文件加载图像。  
  
     在下面的代码示例中，为图像位置设置的路径是**“My Pictures”**文件夹。  大多数运行 Windows 操作系统的计算机将包括该目录。  这还将允许具有最低系统访问级别的用户安全地运行应用程序。  下面的代码示例要求您已经具有添加了 <xref:System.Windows.Forms.PictureBox> 控件的窗体。  
  
    ```vb  
    ' Replace the image named below  
    ' with an icon of your own choosing.  
    PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.MyPictures) _  
       & "\Image.gif")  
  
    ```  
  
    ```csharp  
    // Replace the image named below  
    // with an icon of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    pictureBox1.Image = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.MyPictures)  
       + @"\Image.gif");  
  
    ```  
  
    ```cpp  
    // Replace the image named below  
    // with an icon of your own choosing.  
    pictureBox1->Image = Image::FromFile(String::Concat  
       (System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::MyPictures),  
       "\\Image.gif"));  
    ```  
  
## 请参阅  
 <xref:System.Drawing.Image.FromFile%2A>   
 <xref:System.Drawing.Image>   
 <xref:System.Windows.Forms.Control.BackgroundImage%2A>