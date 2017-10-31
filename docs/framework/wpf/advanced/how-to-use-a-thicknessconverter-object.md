---
title: "如何：使用 ThicknessConverter 对象 | Microsoft Docs"
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
  - "边框粗细"
  - "ThicknessConverter 对象"
ms.assetid: 52682194-d7fd-499c-8005-73fcc84e7b2c
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用 ThicknessConverter 对象
## 示例  
 本示例演示如何创建 <xref:System.Windows.ThicknessConverter> 的实例，并用它来更改边框的粗细。  
  
 此示例定义了一个称为 `changeThickness` 的自定义方法，此方法首先将单独 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件中定义的 <xref:System.Windows.Controls.ListBoxItem> 的内容转换为 <xref:System.Windows.Thickness> 的实例，然后再将该内容转换为 <xref:System.String>。  此方法将 <xref:System.Windows.Controls.ListBoxItem> 传递给 <xref:System.Windows.ThicknessConverter> 对象，该对象将 <xref:System.Windows.Controls.ListBoxItem> 的 <xref:System.Windows.Controls.ContentControl.Content%2A> 转换为 <xref:System.Windows.Thickness> 的实例。  此值然后作为 <xref:System.Windows.Controls.Border> 的 <xref:System.Windows.Controls.Border.BorderThickness%2A> 属性值进行回传。  
  
 此示例不运行。  
  
 [!code-csharp[ThicknessConverter#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ThicknessConverter/CSharp/Window1.xaml.cs#1)]
 [!code-vb[ThicknessConverter#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ThicknessConverter/VisualBasic/Window1.xaml.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Thickness>   
 <xref:System.Windows.ThicknessConverter>   
 <xref:System.Windows.Controls.Border>   
 [How to: Change the Margin Property](http://msdn.microsoft.com/zh-cn/8a313efd-5f99-4097-b4c1-8fa49d8379a2)   
 [How to: Convert a ListBoxItem to a new Data Type](http://msdn.microsoft.com/zh-cn/7a080b88-184e-4b27-bb61-d42bafba9727)   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)