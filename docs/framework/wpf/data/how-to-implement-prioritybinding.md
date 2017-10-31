---
title: "如何：实现 PriorityBinding | Microsoft Docs"
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
  - "类, PriorityBinding"
  - "Data Binding — 数据绑定, PriorityBinding 类"
  - "PriorityBinding 类"
ms.assetid: d63b65ab-b3e9-4322-9aa8-1450f8d89532
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：实现 PriorityBinding
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的 <xref:System.Windows.Data.PriorityBinding> 通过指定绑定列表来工作。  该绑定列表按照优先级由高到低排序。  如果在处理具有最高优先级的绑定时成功返回了一个值，则说明永远不需要处理该列表中的其他绑定。  这有可能发生在以下情况下：当具有最高优先级的绑定需要很长时间来计算时，将使用能够成功返回一个值的次高优先级，直到具有较高优先级的绑定成功返回一个值。  
  
## 示例  
 为了演示 <xref:System.Windows.Data.PriorityBinding> 的工作方式，我们创建了具有以下三个属性的 `AsyncDataSource` 对象：`FastDP`、`SlowerDP` 和 `SlowestDP`。  
  
 `FastDP` 的 get 访问器返回 `_fastDP` 数据成员的值。  
  
 `SlowerDP` 的 get 访问器等待 3 秒钟之后返回 `_slowerDP` 数据成员的值。  
  
 `SlowestDP` 的 get 访问器等待 5 秒钟之后返回 `_slowestDP` 数据成员的值。  
  
> [!NOTE]
>  此示例仅供演示使用。  [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] 准则建议您定义运算速度比字段集慢多个数量级的属性。  有关更多信息，请参见[NIB: Choosing Between Properties and Methods](http://msdn.microsoft.com/zh-cn/55825e8f-7e2e-448a-9505-7217cc91b1af)。  
  
 [!code-csharp[PriorityBinding#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml.cs#1)]
 [!code-vb[PriorityBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PriorityBinding/VisualBasic/AsyncDataSource.vb#1)]  
  
 <xref:System.Windows.Controls.TextBlock.Text%2A> 属性使用 <xref:System.Windows.Data.PriorityBinding> 绑定到上面的 `AsyncDS`：  
  
 [!code-xml[PriorityBinding#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml#2)]  
  
 当绑定引擎处理 <xref:System.Windows.Data.Binding> 对象时，它会首先处理第一个 <xref:System.Windows.Data.Binding> 元素，该元素绑定到 `SlowestDP` 属性。  该 <xref:System.Windows.Data.Binding> 经过处理之后，它不会立即成功返回一个值，因为它会等待 5 秒钟时间，以便对下一个 <xref:System.Windows.Data.Binding> 元素进行处理。  下一个 <xref:System.Windows.Data.Binding> 不会立即成功返回一个值，因为它要等待 3 秒钟时间。  绑定引擎随后会转至下一个 <xref:System.Windows.Data.Binding> 元素，该元素绑定到 `FastDP` 属性。  该 <xref:System.Windows.Data.Binding> 返回值“Fast Value”（快值）。  <xref:System.Windows.Controls.TextBlock> 现在显示值“Fast Value”（快值）。  
  
 在 3 秒钟之后，`SlowerDP` 属性将返回值“Slower Value”（较慢的值）。  <xref:System.Windows.Controls.TextBlock> 随后显示值“Slower Value”（较慢的值）。  
  
 在 5 秒钟之后，`SlowestDP` 属性将返回值“Slowest Value”（最慢的值）。  由于该绑定最先列出，因此它的优先级最高。  <xref:System.Windows.Controls.TextBlock> 现在显示值“Slowest Value”（最慢的值）。  
  
 有关可以将哪种情况视为能够从绑定中成功返回值的信息，请参见 <xref:System.Windows.Data.PriorityBinding>。  
  
## 请参阅  
 <xref:System.Windows.Data.Binding.IsAsync%2A?displayProperty=fullName>   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)