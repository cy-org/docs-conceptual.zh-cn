---
title: "如何：向 Viewbox 的内容应用 Stretch 属性 | Microsoft Docs"
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
  - "控件, Viewbox"
  - "Stretch 属性"
  - "StretchDirection 属性"
  - "Viewbox 控件"
ms.assetid: b9c22ef4-bce4-4300-9e0c-8260b7db83cc
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：向 Viewbox 的内容应用 Stretch 属性
## 示例  
 此示例演示如何更改 <xref:System.Windows.Controls.Viewbox> 的 <xref:System.Windows.Controls.Viewbox.StretchDirection%2A> 和 <xref:System.Windows.Controls.Viewbox.Stretch%2A> 属性的值。  
  
 第一个示例使用 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 定义 <xref:System.Windows.Controls.Viewbox> 元素。  它分配了 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 和 <xref:System.Windows.FrameworkElement.MaxHeight%2A>，值均为 400。  下面的示例在 <xref:System.Windows.Controls.Viewbox> 中嵌套一个 <xref:System.Windows.Controls.Image> 元素。  对应于 <xref:System.Windows.Controls.Viewbox.Stretch%2A> 和 <xref:System.Windows.Controls.StretchDirection> 枚举的属性值的 <xref:System.Windows.Controls.Button> 元素控制嵌套 <xref:System.Windows.Controls.Image> 的拉伸行为。  
  
 [!code-xml[viewboxStretchLayoutSamp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml#1)]  
  
 以下代码隐藏文件处理上述 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 示例定义的 <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  
  
 [!code-csharp[viewboxStretchLayoutSamp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml.cs#2)]
 [!code-vb[viewboxStretchLayoutSamp#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/viewboxStretchLayoutSamp/VisualBasic/Window1.xaml.vb#2)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Viewbox>   
 <xref:System.Windows.Media.Stretch>   
 <xref:System.Windows.Controls.StretchDirection>