---
title: "如何：获取 ListBoxItem | Microsoft Docs"
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
  - "ListBox 控件, 获取 ListBoxItem"
  - "ListBoxItem"
ms.assetid: da877c6f-5fd8-40cb-8909-225cbfd99aa5
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：获取 ListBoxItem
如果需要获取 <xref:System.Windows.Controls.ListBox> 中特定索引位置的特定 <xref:System.Windows.Controls.ListBoxItem>，可以使用 <xref:System.Windows.Controls.ItemContainerGenerator>。  
  
## 示例  
 下面的示例演示 <xref:System.Windows.Controls.ListBox> 和它的项。  
  
 [!code-xml[ListBoxItems#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml#1)]  
  
 下面的示例演示如何通过在 <xref:System.Windows.Controls.ItemContainerGenerator> 的 <xref:System.Windows.Controls.ItemContainerGenerator.ContainerFromIndex%2A> 属性中指定项索引来检索项。  
  
 [!code-csharp[ListBoxItems#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ListBoxItems#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxItems/VisualBasic/Window1.xaml.vb#2)]  
  
 在检索过列表框项后，可以显示该项的内容，如下面的示例所示。  
  
 [!code-csharp[ListBoxItems#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml.cs#3)]
 [!code-vb[ListBoxItems#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxItems/VisualBasic/Window1.xaml.vb#3)]