---
title: "如何：使用 FontSizeConverter 类 | Microsoft Docs"
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
  - "FontSizeConverter 对象"
  - "版式, FontSizeConverter 对象"
ms.assetid: 3b0592bd-7223-4860-a108-a5d72f3a9178
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用 FontSizeConverter 类
## 示例  
 此示例演示如何创建 <xref:System.Windows.FontSizeConverter> 的实例，并用它来更改字号。  
  
 此示例定义一个名为 `changeSize` 的自定义方法，该方法会将 <xref:System.Windows.Controls.ListBoxItem>（在单独的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件中定义）的内容转换为 <xref:System.Double> 的实例，然后再转换为 <xref:System.String>。  此方法将 <xref:System.Windows.Controls.ListBoxItem> 传递给 <xref:System.Windows.FontSizeConverter> 对象，该对象将 <xref:System.Windows.Controls.ListBoxItem> 的 <xref:System.Windows.Controls.ContentControl.Content%2A> 转换为 <xref:System.Double> 的实例。  然后，此值作为 <xref:System.Windows.Controls.TextBlock> 元素的 <xref:System.Windows.Controls.TextBlock.FontSize%2A> 属性值进行回传。  
  
 此示例还定义了名为 `changeFamily` 的第二个自定义方法。  此方法将 <xref:System.Windows.Controls.ListBoxItem> 的 <xref:System.Windows.Controls.ContentControl.Content%2A> 转换为 <xref:System.String>，然后将该值回传给 <xref:System.Windows.Controls.TextBlock> 元素的 <xref:System.Windows.Controls.TextBlock.FontFamily%2A> 属性。  
  
 此示例不运行。  
  
 [!code-csharp[FontSizeConverter#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSizeConverter/CSharp/Window1.xaml.cs#1)]  
  
## 请参阅  
 <xref:System.Windows.FontSizeConverter>