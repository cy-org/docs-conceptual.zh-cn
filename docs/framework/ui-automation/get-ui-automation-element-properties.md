---
title: "Get UI Automation Element Properties | Microsoft Docs"
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
  - "properties, retrieving"
  - "UI Automation, retrieving properties of elements"
ms.assetid: 09576b1a-291f-435c-980e-dee32d899ae1
caps.latest.revision: 5
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 5
---
# Get UI Automation Element Properties
> [!NOTE]
>  本文档的目标读者是欲使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]类的 .NET Framework 开发人员。  有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新信息，请参见 [Windows Automation API: UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746)（Windows 自动化 API：UI 自动化）。  
  
 本主题演示如何检索 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]元素的属性。  
  
### 获取当前的属性值  
  
1.  获取希望得到其属性的 <xref:System.Windows.Automation.AutomationElement>。  
  
2.  调用 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A>，或者检索 <xref:System.Windows.Automation.AutomationElement.Current%2A> 属性结构并从它的某个成员获取值。  
  
### 获取缓存的属性值  
  
1.  获取希望得到其属性的 <xref:System.Windows.Automation.AutomationElement>。  该属性必须已经在 <xref:System.Windows.Automation.CacheRequest> 中指定。  
  
2.  调用 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A>，或者检索 <xref:System.Windows.Automation.AutomationElement.Cached%2A> 属性结构并从它的某个成员获取值。  
  
## 示例  
 下面的示例演示各种用来检索 <xref:System.Windows.Automation.AutomationElement> 的当前属性的方法。  
  
 [!code-csharp[UIAClient_snip#170](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#170)]
 [!code-vb[UIAClient_snip#170](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#170)]  
  
## 请参阅  
 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)   
 [Caching in UI Automation Clients](../../../docs/framework/ui-automation/caching-in-ui-automation-clients.md)