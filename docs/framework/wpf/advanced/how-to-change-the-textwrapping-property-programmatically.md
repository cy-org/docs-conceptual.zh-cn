---
title: "如何：以编程方式更改 TextWrapping 属性 | Microsoft Docs"
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
  - "文档, 以编程方式更改 TextWrapping 属性"
  - "TextWrapping 属性, 以编程方式更改"
ms.assetid: 30d25554-4c82-4df9-a8d6-35683a4a13bb
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：以编程方式更改 TextWrapping 属性
## 示例  
 下面的代码示例演示如何以编程方式更改 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> 属性的值。  
  
 三个 <xref:System.Windows.Controls.Button> 元素放置在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的 <xref:System.Windows.Controls.StackPanel> 元素内。<xref:System.Windows.Controls.Button> 的每个 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件都对应于代码中的一个事件处理程序。  单击按钮后，事件处理程序将使用其将向 `txt2` 应用的 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> 值的相同名称。  此外，还会更新 `txt1`（[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中未显示的 <xref:System.Windows.Controls.TextBlock>）中的文本，以反映属性中的变化。  
  
 [!code-xml[TextWrapProperty#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextWrapProperty/VisualBasic/Pane1.xaml#1)]  
  
 [!code-csharp[TextWrapProperty#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextWrapProperty/CSharp/Window1.xaml.cs#2)]
 [!code-vb[TextWrapProperty#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextWrapProperty/VisualBasic/Pane1.xaml.vb#2)]  
  
## 请参阅  
 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A>   
 <xref:System.Windows.TextWrapping>