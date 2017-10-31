---
title: "如何：清除绑定 | Microsoft Docs"
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
  - "绑定, 清除"
  - "清除绑定"
  - "Data Binding — 数据绑定, 清除绑定"
ms.assetid: 73962a93-32a9-4bcd-9240-bcfbb239093a
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：清除绑定
此示例演示如何从对象清除绑定。  
  
## 示例  
 若要从对象的个别属性清除绑定，请按下例所示调用 <xref:System.Windows.Data.BindingOperations.ClearBinding%2A>。  下面的示例会从 *mytext* 的 <xref:System.Windows.Controls.TextBlock.TextProperty> 中移除绑定，前者是一个 <xref:System.Windows.Controls.TextBlock> 对象。  
  
 [!code-csharp[CodeOnlyBinding#ClearBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#clearbinding)]
 [!code-vb[CodeOnlyBinding#ClearBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#clearbinding)]  
  
 清除绑定会移除绑定，这样[依赖项属性](GTMT)的值会更改为过去尚未绑定时的值。  此值可以是默认值、继承值或来自模板绑定的值。  
  
 若要从对象的所有可能属性中清除绑定，请使用 <xref:System.Windows.Data.BindingOperations.ClearAllBindings%2A>。  
  
## 请参阅  
 <xref:System.Windows.Data.BindingOperations>   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)