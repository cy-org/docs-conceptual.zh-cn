---
title: "如何：创建和使用 GridLengthConverter 对象 | Microsoft Docs"
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
  - "Grid 控件, 创建, GridLengthConverter 对象"
ms.assetid: 5ab75911-e36a-4825-80e4-081c57e8e182
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：创建和使用 GridLengthConverter 对象
## 示例  
 下面的示例演示如何创建和使用 <xref:System.Windows.GridLengthConverter> 的实例。  此示例定义了一个名为 `changeCol` 的自定义方法，该方法将 <xref:System.Windows.Controls.ListBoxItem> 传递给 <xref:System.Windows.GridLengthConverter>，它将 <xref:System.Windows.Controls.ListBoxItem> 的<xref:System.Windows.Controls.ContentControl.Content%2A>转换为 <xref:System.Windows.GridLength> 的实例。  转换后的值然后作为 <xref:System.Windows.Controls.ColumnDefinition> 元素的 <xref:System.Windows.Controls.ColumnDefinition.Width%2A> 属性值进行回传。  
  
 此示例还定义了名为 `changeColVal` 的第二个自定义方法。  此自定义方法将<xref:System.Windows.Controls.Slider>的<xref:System.Windows.Controls.Primitives.RangeBase.Value%2A>转换为<xref:System.String>，然后将该值作为元素的 <xref:System.Windows.Controls.ColumnDefinition.Width%2A> 回传给 <xref:System.Windows.Controls.ColumnDefinition>。  
  
 请注意，<xref:System.Windows.Controls.ListBoxItem> 的内容在单独的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件中定义。  
  
 [!code-csharp[gridlengthConverterGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridlengthConverterGrid/CSharp/Window1.xaml.cs#1)]
 [!code-vb[gridlengthConverterGrid#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gridlengthConverterGrid/VisualBasic/Window1.xaml.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.GridLengthConverter>   
 <xref:System.Windows.GridLength>