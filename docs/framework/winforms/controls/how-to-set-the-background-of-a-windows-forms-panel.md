---
title: "如何：设置 Windows 窗体面板的背景 | Microsoft Docs"
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
  - "背景色, Windows 窗体 Panel 控件"
  - "背景图像, Windows 窗体 Panel 控件"
  - "颜色, Windows 窗体 Panel 控件"
  - "Panel 控件 [Windows 窗体], 背景"
ms.assetid: 096cbd8d-45cc-47b8-b1ef-a27f60ea8be0
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：设置 Windows 窗体面板的背景
Windows 窗体 <xref:System.Windows.Forms.Panel> 控件既可以显示背景颜色又可以显示背景图像。  <xref:System.Windows.Forms.Control.BackColor%2A> 属性为所包含的控件（如标签和单选按钮）设置背景颜色。  如果未设置 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 属性，则为 <xref:System.Windows.Forms.Control.BackColor%2A> 选择的颜色将充满整个面板。  如果设置了 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 属性，则该图像将显示在所包含的控件的后面。  
  
### 以编程方式设置背景  
  
1.  将面板的 <xref:System.Windows.Forms.Control.BackColor%2A> 属性设置为 <xref:System.Drawing.Color?displayProperty=fullName> 类型的值。  
  
    ```vb  
    Panel1.BackColor = Color.AliceBlue  
  
    ```  
  
    ```csharp  
    panel1.BackColor = Color.AliceBlue;  
  
    ```  
  
    ```cpp  
    panel1->BackColor = Color::AliceBlue;  
    ```  
  
2.  使用 <xref:System.Drawing.Image?displayProperty=fullName> 类的 <xref:System.Drawing.Image.FromFile%2A> 方法设置面板的 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 属性。  
  
    ```vb  
    ' You should replace the bolded image   
    ' in the sample below with an image of your own choosing.  
    Panel1.BackgroundImage = Image.FromFile _  
        (System.Environment.GetFolderPath _  
        (System.Environment.SpecialFolder.Personal) _  
        & "\Image.gif")  
  
    ```  
  
    ```csharp  
    // You should replace the bolded image   
    // in the sample below with an image of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    panel1.BackgroundImage = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
  
    ```  
  
    ```cpp  
    // You should replace the bolded image   
    // in the sample below with an image of your own choosing.  
    panel1->BackgroundImage = Image::FromFile(String::Concat(  
       System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\Image.gif"));  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.BackColor%2A>   
 <xref:System.Windows.Forms.Control.BackgroundImage%2A>   
 [Panel 控件](../../../../docs/framework/winforms/controls/panel-control-windows-forms.md)   
 [Panel 控件概述](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)