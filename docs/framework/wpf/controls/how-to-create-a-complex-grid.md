---
title: "如何：创建复杂网格 | Microsoft Docs"
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
  - "日历, 创建"
  - "Grid 控件, 创建, 复杂网格"
  - "月历, 创建"
ms.assetid: 4ce3040a-a156-4364-9596-98ca1eca5550
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：创建复杂网格
本示例演示如何使用<xref:System.Windows.Controls.Grid>创建外观类似于月历的布局。  
  
## 示例  
 下面的示例通过使用 <xref:System.Windows.Controls.RowDefinition> 和 <xref:System.Windows.Controls.ColumnDefinition> 类来定义八个行和八个列。  它使用 <xref:System.Windows.Controls.Grid.ColumnSpan%2A?displayProperty=fullName> 和 <xref:System.Windows.Controls.Grid.RowSpan%2A?displayProperty=fullName> 附加属性以及用于填充各个列和行的背景的 <xref:System.Windows.Shapes.Rectangle> 元素。  此设计是可行的，因为<xref:System.Windows.Controls.Grid>的每个单元格中可以存在多个元素，这是<xref:System.Windows.Controls.Grid>与<xref:System.Windows.Documents.Table>的主要区别。  
  
 此示例使用垂直渐变来<xref:System.Windows.Shapes.Shape.Fill%2A>列和行，以提高日历的可视形式和可读性。  具有样式的 <xref:System.Windows.Controls.TextBlock> 元素代表日期和星期几。  <xref:System.Windows.Controls.TextBlock> 元素使用在应用程序的样式中定义的 <xref:System.Windows.FrameworkElement.Margin%2A> 属性和对齐属性，以绝对方式定位在其单元格内。  
  
 [!code-xml[GridComplex#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridComplex/CS/default.xaml#1)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Grid>   
 <xref:System.Windows.Documents.TableCell>   
 [使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [表概述](../../../../docs/framework/wpf/advanced/table-overview.md)