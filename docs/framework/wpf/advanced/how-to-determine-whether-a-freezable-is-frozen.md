---
title: "如何：确定 Freezable 是否处于冻结状态 | Microsoft Docs"
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
  - "Freezable 对象, 确定是否冻结"
  - "IsFrozen 属性"
ms.assetid: 92e58baa-ee12-4a9e-ac3a-ca458807a8b2
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：确定 Freezable 是否处于冻结状态
此示例演示如何确定 <xref:System.Windows.Freezable> 对象是否处于冻结状态。  如果尝试修改冻结的 <xref:System.Windows.Freezable> 对象，该对象将引发 <xref:System.InvalidOperationException>。  为了避免引发此异常，请使用 <xref:System.Windows.Freezable> 对象的 <xref:System.Windows.Freezable.IsFrozen%2A> 属性来确定对象是否处于冻结状态。  
  
## 示例  
 下面的示例将冻结 <xref:System.Windows.Media.SolidColorBrush>，然后通过使用 <xref:System.Windows.Freezable.IsFrozen%2A> 属性对其进行测试，以确定它是否处于冻结状态。  
  
 [!code-csharp[freezablesample_procedural#CheckIsFrozenExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#checkisfrozenexample)]
 [!code-vb[freezablesample_procedural#CheckIsFrozenExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#checkisfrozenexample)]  
  
 有关 <xref:System.Windows.Freezable> 对象的更多信息，请参见[Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Freezable>   
 <xref:System.Windows.Freezable.IsFrozen%2A>   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/base-elements-how-to-topics.md)