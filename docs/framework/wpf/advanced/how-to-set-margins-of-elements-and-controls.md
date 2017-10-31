---
title: "如何：设置元素和控件的边距 | Microsoft Docs"
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
  - "Margin 属性, 设置"
  - "属性, Margin 属性"
  - "设置, Margin 属性"
ms.assetid: 70ebee01-6f87-4352-8dd4-402c65eaaed6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：设置元素和控件的边距
本示例介绍如何通过在代码隐藏文件中更改边距的任何现有属性值来设置 <xref:System.Windows.FrameworkElement.Margin%2A> 属性。  <xref:System.Windows.FrameworkElement.Margin%2A> 属性是 <xref:System.Windows.FrameworkElement> 基元素的属性，因此各种控件以及其他元素都会继承该属性。  
  
 本示例以[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 编写，并包含 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 引用的代码隐藏文件。  同时显示了该代码隐藏文件的 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 和 [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)] 版本。  
  
## 示例  
 [!code-xml[FEMarginProgrammatic#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[FEMarginProgrammatic#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml.cs#handler)]
 [!code-vb[FEMarginProgrammatic#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FEMarginProgrammatic/VisualBasic/default.xaml.vb#handler)]