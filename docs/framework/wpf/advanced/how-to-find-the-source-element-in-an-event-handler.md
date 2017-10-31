---
title: "如何：在事件处理程序中查找源元素 | Microsoft Docs"
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
  - "事件处理程序, 查找资源元素"
  - "事件处理程序中的源元素"
ms.assetid: 85f71c5a-b714-4c65-9711-7d905c2bbe98
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：在事件处理程序中查找源元素
本示例演示如何在事件处理程序中查找源元素。  
  
## 示例  
 下面的示例演示一个在代码隐藏文件中声明的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序。  当用户单击该处理程序所附加到的按钮时，处理程序将更改属性值。  处理程序代码使用在事件参数中报告的路由事件数据的 <xref:System.Windows.RoutedEventArgs.Source%2A> 属性来更改 <xref:System.Windows.RoutedEventArgs.Source%2A> 元素的 <xref:System.Windows.FrameworkElement.Width%2A> 属性值。  
  
 [!code-xml[RoutedEventSource#XAMLHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventSource/CSharp/default.xaml#xamlhandler)]  
  
 [!code-csharp[RoutedEventSource#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventSource/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventSource#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventSource/VisualBasic/default.xaml.vb#handler)]  
  
## 请参阅  
 <xref:System.Windows.RoutedEventArgs>   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/events-how-to-topics.md)