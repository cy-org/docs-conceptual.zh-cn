---
title: "如何：使 Freezable 成为只读 | Microsoft Docs"
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
  - "Freezable 对象, 使只读"
ms.assetid: 6c544b7d-d3c9-4736-aa90-4b8728234ccb
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使 Freezable 成为只读
本示例演示如何通过调用其 <xref:System.Windows.Freezable.Freeze%2A> 方法使 <xref:System.Windows.Freezable> 变为只读。  
  
 如果以下任何一个对象相关条件为 `true`，则无法冻结 <xref:System.Windows.Freezable> 对象：  
  
-   它有动画或数据绑定的属性。  
  
-   它有由动态资源设置的属性。  有关动态资源的更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
-   它包含无法冻结的 <xref:System.Windows.Freezable> 子对象。  
  
 如果这些条件对于 <xref:System.Windows.Freezable> 对象为 `false`，并且您不希望修改它，请将其冻结以提高性能。  
  
## 示例  
 下面的示例冻结 <xref:System.Windows.Media.SolidColorBrush>（它属于 <xref:System.Windows.Freezable> 对象类型）。  
  
 [!code-csharp[freezablesample_procedural#FreezeExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#freezeexample1)]
 [!code-vb[freezablesample_procedural#FreezeExample1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#freezeexample1)]  
  
 有关 <xref:System.Windows.Freezable> 对象的更多信息，请参见[Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Freezable>   
 <xref:System.Windows.Freezable.CanFreeze%2A>   
 <xref:System.Windows.Freezable.Freeze%2A>   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/base-elements-how-to-topics.md)