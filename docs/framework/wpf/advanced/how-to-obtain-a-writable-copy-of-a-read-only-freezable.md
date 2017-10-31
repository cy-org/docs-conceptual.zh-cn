---
title: "如何：获取只读 Freezable 的可写副本 | Microsoft Docs"
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
  - "克隆 Freezable 对象"
  - "Freezable 对象, 可修改的克隆"
ms.assetid: d028de61-bbe9-4d62-b656-8fe3b1b2ca24
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：获取只读 Freezable 的可写副本
此示例显示如何使用 <xref:System.Windows.Freezable.Clone%2A> 方法来创建只读 <xref:System.Windows.Freezable> 的可写副本。  
  
 在将 <xref:System.Windows.Freezable> 对象标记为只读（“冻结”）后，便无法对其进行修改。  但是，可以使用 <xref:System.Windows.Freezable.Clone%2A> 方法来创建冻结对象的可修改克隆。  
  
## 示例  
 以下示例将创建冻结 <xref:System.Windows.Media.SolidColorBrush> 对象的可修改克隆。  
  
 [!code-csharp[freezablesample_procedural#CloneExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#cloneexample)]
 [!code-vb[freezablesample_procedural#CloneExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#cloneexample)]  
  
 有关 <xref:System.Windows.Freezable> 对象的更多信息，请参见[Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Freezable>   
 <xref:System.Windows.Freezable.CloneCurrentValue%2A>   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/base-elements-how-to-topics.md)