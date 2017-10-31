---
title: "如何：处理 Loaded 事件 | Microsoft Docs"
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
  - "事件, Loaded"
  - "Loaded 事件"
  - "XAML, Loaded 事件"
ms.assetid: 0cf8d003-8441-4df4-807a-6db09347e829
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：处理 Loaded 事件
本示例演示如何处理 <xref:System.Windows.FrameworkElement.Loaded?displayProperty=fullName> 事件以及处理该事件的相应方案。  处理程序在页面加载时创建一个 <xref:System.Windows.Controls.Button>。  
  
## 示例  
 下面的示例将[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 与代码隐藏文件一起使用。  
  
 [!code-xml[FELoaded#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FELoaded/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[FELoaded#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FELoaded/CSharp/default.xaml.cs#handler)]
 [!code-vb[FELoaded#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FELoaded/VisualBasic/default.xaml.vb#handler)]  
  
## 请参阅  
 <xref:System.Windows.FrameworkElement>   
 [对象生存期事件](../../../../docs/framework/wpf/advanced/object-lifetime-events.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/base-elements-how-to-topics.md)