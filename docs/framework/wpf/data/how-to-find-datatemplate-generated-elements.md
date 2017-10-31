---
title: "如何：查找由 DataTemplate 生成的元素 | Microsoft Docs"
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
  - "DataTemplate"
  - "查找 DataTemplate 元素"
ms.assetid: bfcd564e-5e9e-451e-8641-a9b5c3cfac90
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：查找由 DataTemplate 生成的元素
下面的示例演示如何查找由 <xref:System.Windows.DataTemplate> 生成的元素。  
  
## 示例  
 在本示例中，有一个绑定到某些 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据的 <xref:System.Windows.Controls.ListBox>：  
  
 [!code-xml[FindGeneratedItems#LB](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml#lb)]  
  
 <xref:System.Windows.Controls.ListBox> 使用以下 <xref:System.Windows.DataTemplate>：  
  
 [!code-xml[FindGeneratedItems#DT](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml#dt)]  
  
 如果要检索由某个 <xref:System.Windows.Controls.ListBoxItem> 的 <xref:System.Windows.DataTemplate> 生成的 <xref:System.Windows.Controls.TextBlock> 元素，您需要获得 <xref:System.Windows.Controls.ListBoxItem>，在该 <xref:System.Windows.Controls.ListBoxItem> 内查找 <xref:System.Windows.Controls.ContentPresenter>，然后对在该 <xref:System.Windows.Controls.ContentPresenter> 上设置的 <xref:System.Windows.DataTemplate> 调用 <xref:System.Windows.FrameworkTemplate.FindName%2A>。  下面的示例演示如何执行这些步骤。  出于演示的目的，本示例创建一个消息框，用于显示由 <xref:System.Windows.DataTemplate> 生成的文本块的文本内容。  
  
 [!code-csharp[FindGeneratedItems#DTFindElement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml.cs#dtfindelement)]
 [!code-vb[FindGeneratedItems#DTFindElement](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindGeneratedItems/VisualBasic/Window1.xaml.vb#dtfindelement)]  
  
 下面是 `FindVisualChild` 的实现，使用的是 <xref:System.Windows.Media.VisualTreeHelper> 方法：  
  
 [!code-csharp[FindGeneratedItems#FVC](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml.cs#fvc)]
 [!code-vb[FindGeneratedItems#FVC](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindGeneratedItems/VisualBasic/Window1.xaml.vb#fvc)]  
  
## 请参阅  
 [如何：查找由 ControlTemplate 生成的元素](../../../../docs/framework/wpf/controls/how-to-find-controltemplate-generated-elements.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [WPF XAML 名称范围](../../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md)   
 [WPF 中的树](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)