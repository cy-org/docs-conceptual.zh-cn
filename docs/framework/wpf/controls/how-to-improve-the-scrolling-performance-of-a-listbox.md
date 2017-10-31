---
title: "如何：提高 ListBox 的滚动性能 | Microsoft Docs"
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
  - "ListBox 控件 [WPF], 提高滚动性能"
  - "ListBox 控件 [WPF], 重用项容器"
ms.assetid: 1e2bf8f3-c8ce-47f7-a400-a7fe11d1a848
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：提高 ListBox 的滚动性能
如果 <xref:System.Windows.Controls.ListBox> 包含很多项，则当用户通过使用鼠标滚轮或拖动滚动条上的滚动块来滚动 <xref:System.Windows.Controls.ListBox> 时，用户界面响应会很慢。  通过将 <xref:System.Windows.Controls.VirtualizingStackPanel.VirtualizationMode%2A?displayProperty=fullName> 附加属性设置为 <xref:System.Windows.Controls.VirtualizationMode>，可以提高 <xref:System.Windows.Controls.ListBox> 在用户滚动时的性能。  
  
## 示例  
  
## 说明  
 下面的示例创建一个 <xref:System.Windows.Controls.ListBox> 并将 <xref:System.Windows.Controls.VirtualizingStackPanel.VirtualizationMode%2A?displayProperty=fullName> 设置为 <xref:System.Windows.Controls.VirtualizationMode> 以提高滚动时的性能。  
  
## 代码  
 [!code-xml[RecycleItemContainerShippets#VirtualizationMode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml#virtualizationmode)]  
  
 下面的示例显示上例所使用的数据。  
  
 [!code-csharp[RecycleItemContainerShippets#ListBoxData](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml.cs#listboxdata)]
 [!code-vb[RecycleItemContainerShippets#ListBoxData](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RecycleItemContainerShippets/visualbasic/window1.xaml.vb#listboxdata)]