---
title: "如何：创建网格元素 | Microsoft Docs"
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
  - "Grid 控件, 创建, 网格实例"
ms.assetid: b2f07626-9df8-43b8-8d36-492f3cb42837
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：创建网格元素
## 示例  
 下面的示例演示如何通过使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 或代码来创建和使用 <xref:System.Windows.Controls.Grid> 的实例。  此示例使用三个 <xref:System.Windows.Controls.ColumnDefinition> 对象和三个 <xref:System.Windows.Controls.RowDefinition> 对象创建一个具有九个单元格的网格，就像在工作表中一样。  每个单元格都包含一个表示数据的 <xref:System.Windows.Controls.TextBlock> 元素，并且首行包含应用了 <xref:System.Windows.Controls.Grid.ColumnSpan%2A> 属性的 <xref:System.Windows.Controls.TextBlock>。  为了显示每个单元格的边界，已启用了 <xref:System.Windows.Controls.Grid.ShowGridLines%2A> 属性。  
  
 [!code-csharp[Grid#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Grid/CSharp/Grid_Code.cs#3)]
 [!code-vb[Grid#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Grid/VisualBasic/grid_vb.vb#3)]
 [!code-xml[Grid#3](../../../../samples/snippets/xaml/VS_Snippets_Wpf/Grid/XAML/default.xaml#3)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Grid>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)