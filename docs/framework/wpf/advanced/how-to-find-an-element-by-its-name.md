---
title: "如何：按名称查找元素 | Microsoft Docs"
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
  - "元素, 按名称查找"
  - "FindName 方法"
ms.assetid: cfa7cf35-8aa2-4060-9454-872ed4af3f0e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：按名称查找元素
此示例介绍如何使用 <xref:System.Windows.FrameworkElement.FindName%2A> 方法按 <xref:System.Windows.FrameworkElement.Name%2A> 值查找元素。  
  
## 示例  
 在本示例中，按名称查找特定元素的方法编写为按钮的事件处理程序。  `stackPanel` 是所搜索的根 <xref:System.Windows.FrameworkElement> 的 <xref:System.Windows.FrameworkElement.Name%2A>，之后示例方法通过将找到的元素强制转换为 <xref:System.Windows.Controls.TextBlock> 并更改 <xref:System.Windows.Controls.TextBlock> 的某个可见 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 属性，以可视方式指示找到的元素。  
  
 [!code-csharp[FEFindName#Find](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEFindName/CSharp/default.xaml.cs#find)]
 [!code-vb[FEFindName#Find](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FEFindName/VisualBasic/default.xaml.vb#find)]