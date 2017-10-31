---
title: "如何：在网格之间共享大小调整属性 | Microsoft Docs"
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
  - "Grid 控件, 共享列的大小调整数据"
  - "Grid 控件, 共享行的大小调整数据"
  - "Grid 控件中的大小调整数据"
ms.assetid: a0535a6f-ff04-4b25-9912-7dd856e11044
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：在网格之间共享大小调整属性
此示例演示如何在 <xref:System.Windows.Controls.Grid> 元素之间共享列和行的大小调整数据，以便使大小调整保持一致。  
  
## 示例  
 下面的示例引入了两个 <xref:System.Windows.Controls.Grid> 元素作为父 <xref:System.Windows.Controls.DockPanel> 的子元素。  <xref:System.Windows.Controls.Grid> 的 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> [附加属性](GTMT)是在父 <xref:System.Windows.Controls.DockPanel> 上定义的。  
  
 以下示例通过使用两个 <xref:System.Windows.Controls.Button> 元素来处理属性值；每个元素表示其中一个布尔属性值。  当 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> 属性值设置为 `true` 时，<xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A> 的每个列或行成员将共享大小调整信息，而不管行或列的内容如何。  
  
 [!code-xml[gridIssharedsizescopeProp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#1)]  
  
 ...  
  
 [!code-xml[gridIssharedsizescopeProp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 下面的代码隐藏示例处理按钮 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件引发的方法。  该示例将这些方法调用的结果写入 <xref:System.Windows.Controls.TextBlock> 元素，这些元素使用相关的 get 方法以字符串的形式输出新属性值。  
  
 [!code-csharp[gridIssharedsizescopeProp#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml.cs#3)]
 [!code-vb[gridIssharedsizescopeProp#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gridIssharedsizescopeProp/VisualBasic/Window1.xaml.vb#3)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Grid>   
 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)