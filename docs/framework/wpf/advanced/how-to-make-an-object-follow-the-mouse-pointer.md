---
title: "如何：使对象跟随鼠标指针移动 | Microsoft Docs"
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
  - "光标（鼠标指针）, 使对象跟随"
  - "跟随鼠标指针（光标）"
  - "鼠标指针（光标）, 使对象跟随"
ms.assetid: 50b20415-14bc-405c-baf3-2fb254fffde3
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：使对象跟随鼠标指针移动
此示例演示当鼠标指针在屏幕上移动时如何更改对象的维度值。  
  
 此示例包括一个用来创建[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件和一个用来创建事件处理程序的代码隐藏文件。  
  
## 示例  
 下面的 [!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)] 创建了 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]（它在 <xref:System.Windows.Controls.StackPanel> 内包括了一个 <xref:System.Windows.Shapes.Ellipse>），并附加了 <xref:System.Windows.UIElement.MouseMove> 事件的事件处理程序。  
  
 [!code-xml[mouseMoveWithPointer#MouseMoveWithPointerXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/mouseMoveWithPointer/CSharp/Window1.xaml#mousemovewithpointerxaml)]  
  
 下面的隐藏代码创建 <xref:System.Windows.UIElement.MouseMove> 事件处理程序。  当鼠标指针移动时，<xref:System.Windows.Shapes.Ellipse> 的高度和宽度随之进行增加和减少。  
  
 [!code-csharp[mouseMoveWithPointer#MouseMovePointerGetPosition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/mouseMoveWithPointer/CSharp/Window1.xaml.cs#mousemovepointergetposition)]
 [!code-vb[mouseMoveWithPointer#MouseMovePointerGetPosition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/mouseMoveWithPointer/VisualBasic/Window1.xaml.vb#mousemovepointergetposition)]  
  
## 请参阅  
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)