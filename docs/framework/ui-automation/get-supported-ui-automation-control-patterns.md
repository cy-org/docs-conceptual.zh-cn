---
title: "获取受支持的 UI 自动化控件模式 | Microsoft Docs"
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
  - "获取控件模式"
  - "获取控件模式的 UI 自动化"
  - "获取控件模式"
ms.assetid: 006c54c9-50bf-48d9-a855-9d62eb95603a
caps.latest.revision: 10
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 10
---
# 获取受支持的 UI 自动化控件模式
> [!NOTE]
>  本文档适用于.NET Framework 开发人员想要使用托管[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中定义的类<xref:System.Windows.Automation>命名空间。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API: UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题演示如何检索控件模式对象从[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]元素。  
  
### <a name="obtain-all-control-patterns"></a>获取所有控件模式  
  
1.  获取<xref:System.Windows.Automation.AutomationElement>其控件模式您感兴趣。  
  
2.  调用<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>来从元素中获取所有控件模式。  
  
> [!CAUTION]
>  强烈建议客户端不使用<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>。 性能会受到严重影响与此方法通过调用<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>内部为每个现有的控件模式。 如果可能，应调用客户端<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>感兴趣的关键模式。  
  
### <a name="obtain-a-specific-control-pattern"></a>获取特定的控件模式  
  
1.  获取<xref:System.Windows.Automation.AutomationElement>其控件模式您感兴趣。  
  
2.  调用<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>或<xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>特定模式的查询。 这些方法很相似，但是，如果未找到该模式， <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>会抛出异常和<xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>返回`false`。  
  
## <a name="example"></a>示例  
 下面的示例检索<xref:System.Windows.Automation.AutomationElement>列表项，并获取<xref:System.Windows.Automation.SelectionItemPattern>从该元素。  
  
 [!code-csharp[UIAClient_snip#103](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#103)]
 [!code-vb[UIAClient_snip#103](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#103)]  
  
## <a name="see-also"></a>另请参阅  
 [客户端 UI 自动化控件模式](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)