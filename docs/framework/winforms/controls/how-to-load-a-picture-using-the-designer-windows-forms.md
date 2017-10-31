---
title: "如何：使用设计器加载图片（Windows 窗体） | Microsoft Docs"
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
  - "窗体, 显示图像"
  - "图像 [Windows 窗体], 在 Windows 窗体上显示"
  - "图片格式"
  - "PictureBox 控件 [Windows 窗体], 添加图片"
  - "pictures, 显示"
ms.assetid: 4dc7b973-afb1-4276-8322-20825af96655
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用设计器加载图片（Windows 窗体）
利用 Windows 窗体 <xref:System.Windows.Forms.PictureBox> 控件，可以在设计时通过将 <xref:System.Windows.Forms.PictureBox.Image%2A> 属性设置为一个有效图片，从而在窗体上加载和显示图片。  下表显示了可接受的文件类型。  
  
|类型|文件扩展名|  
|--------|-----------|  
|位图|.bmp|  
|图标|.ico|  
|GIF|.gif|  
|图元文件|.wmf|  
|JPEG|.jpg|  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时显示图片  
  
1.  在窗体上绘制 <xref:System.Windows.Forms.PictureBox> 控件。  
  
2.  在“属性”窗口中，选择 <xref:System.Windows.Forms.PictureBox.Image%2A> 属性，然后单击省略号按钮以显示**“打开”**对话框。  
  
3.  如果要查找特定文件类型（例如 .gif 文件），请在**“文件类型”**框中选择相应的类型。  
  
4.  选择要显示的文件。  
  
### 在设计时清除图片  
  
1.  在**“属性”**窗口中，选择 <xref:System.Windows.Forms.PictureBox.Image%2A> 属性，并右击出现在图像对象名称左边的小缩略图像。  选择**“重置”**。  
  
## 请参阅  
 <xref:System.Windows.Forms.PictureBox>   
 [PictureBox 控件概述](../../../../docs/framework/winforms/controls/picturebox-control-overview-windows-forms.md)   
 [如何：在运行时修改图片的大小或位置](../../../../docs/framework/winforms/controls/how-to-modify-the-size-or-placement-of-a-picture-at-run-time-windows-forms.md)   
 [如何：在运行时设置图片](../../../../docs/framework/winforms/controls/how-to-set-pictures-at-run-time-windows-forms.md)   
 [PictureBox 控件](../../../../docs/framework/winforms/controls/picturebox-control-windows-forms.md)