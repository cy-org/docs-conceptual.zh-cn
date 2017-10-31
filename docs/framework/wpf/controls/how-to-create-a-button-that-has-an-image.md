---
title: "如何：创建包含图像的按钮 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Button 控件 [WPF], 创建"
ms.assetid: 607a193c-4098-4dd8-8dc0-51256cec2020
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：创建包含图像的按钮
本示例演示如何在 <xref:System.Windows.Controls.Button> 上包含一个图像。  
  
## 示例  
 下面的示例创建两个 <xref:System.Windows.Controls.Button> 控件。  一个 <xref:System.Windows.Controls.Button> 包含文本，另一个包含图像。  图像位于一个名为 data 的文件夹中，该文件夹是示例的项目文件夹的子文件夹。  当用户单击包含图像的 <xref:System.Windows.Controls.Button> 时，另一个 <xref:System.Windows.Controls.Button> 的背景和文本将发生变化。  
  
 此示例使用标记创建 <xref:System.Windows.Controls.Button> 控件，但使用代码编写 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序。  
  
 [!code-xml[BtnColor#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BtnColor/CSharp/Pane1.xaml#4)]  
  
 [!code-csharp[BtnColor#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BtnColor/CSharp/Pane1.xaml.cs#6)]
 [!code-vb[BtnColor#6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BtnColor/VisualBasic/Pane1.xaml.vb#6)]  
  
## 请参阅  
 [控件](../../../../docs/framework/wpf/controls/index.md)   
 [控件库](../../../../docs/framework/wpf/controls/control-library.md)