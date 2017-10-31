---
title: "Find a UI Automation Element for a List Item | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "list items, finding elements for"
  - "elements, finding for list items"
  - "UI Automation, finding elements for List items"
ms.assetid: c326ad2b-2144-4f64-ae4c-d850c74f95c5
caps.latest.revision: 5
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 5
---
# Find a UI Automation Element for a List Item
> [!NOTE]
>  本文档的目标读者是欲使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]类的 .NET Framework 开发人员。  有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新信息，请参见 [Windows Automation API: UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746)（Windows 自动化 API：UI 自动化）。  
  
 本主题演示在已知某个列表项的索引的情况下如何在列表中检索该项的 <xref:System.Windows.Automation.AutomationElement>。  
  
## 示例  
 下面的示例演示从列表中检索指定项的两种方法：一种方法是使用 <xref:System.Windows.Automation.TreeWalker>，另一种方法是使用 <xref:System.Windows.Automation.AutomationElement.FindAll%2A>。  
  
 对于 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 控件，第一种方法往往更快，但对于 [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)] 控件，第二种方法更快。  
  
 [!code-csharp[UIAClient_snip#184](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#184)]
 [!code-vb[UIAClient_snip#184](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#184)]  
  
## 请参阅  
 [Obtaining UI Automation Elements](../../../docs/framework/ui-automation/obtaining-ui-automation-elements.md)