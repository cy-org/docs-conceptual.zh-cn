---
title: "UI Automation Control Patterns for Clients | Microsoft Docs"
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
  - "UI Automation, control patterns for clients"
  - "control patterns, UI Automation clients"
ms.assetid: 571561d8-5f49-43a9-a054-87735194e013
caps.latest.revision: 24
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 24
---
# UI Automation Control Patterns for Clients
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 此概述介绍 UI 自动化客户端的控件模式。 它包括有关 UI 自动化客户端如何使用控件模式访问 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 相关信息的信息。  
  
 控件模式提供了一种方法，用于独立于控件类型或控件的外观对控件的功能进行分类和公开。 UI 自动化客户端可以检查 <xref:System.Windows.Automation.AutomationElement> 以确定哪些控件模式受支持并确保控件的行为。  
  
 有关控件模式的完整列表，请参阅 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)。  
  
<a name="uiautomation_getting_control_patterns"></a>   
## 获取控件模式  
 客户端通过调用 <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A?displayProperty=fullName> 或 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A?displayProperty=fullName> 从 <xref:System.Windows.Automation.AutomationElement> 检索控件模式。  
  
 客户端可以使用 <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A> 方法或单个 `IsPatternAvailable` 属性（例如 <xref:System.Windows.Automation.AutomationElement.IsTextPatternAvailableProperty>）来确定一个模式或一组模式是否在 <xref:System.Windows.Automation.AutomationElement> 上受支持。 但是，尝试获取控件模式并针对 `null` 引用进行测试比检查支持的属性并检索控件模式更高效，因为这样进行的跨进程调用更少。  
  
 以下示例演示如何从 <xref:System.Windows.Automation.AutomationElement> 获取 <xref:System.Windows.Automation.TextPattern> 控件模式。  
  
 [!code-csharp[UIATextPattern_snip#1037](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIATextPattern_snip/CSharp/SearchWindow.cs#1037)]  
  
<a name="uiautomation_properties_on_control_patterns"></a>   
## 检索控件模式上的属性  
 客户端可以通过调用 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=fullName> 或 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=fullName> 并将返回的对象强制转换为适当类型，来检索控件模式上的属性值。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性的详细信息，请参阅 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)。  
  
 除了 `GetPropertyValue` 方法之外，还可以通过 [!INCLUDE[TLA#tla_clr](../../../includes/tlasharptla-clr-md.md)] 访问器检索属性值以访问模式上的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性。  
  
<a name="uiautomation_with_variable_patterns"></a>   
## 具有可变模式的控件  
 某些控件类型支持不同的模式，具体取决于它们的状态或使用控件的方式。 可以具有可变模式的控件示例包括列表视图（缩略图、图块、图标、列表、详细信息）、[!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] 图表（饼图、折线图、条形图、带有公式的单元格值）、[!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] 的文档区域（正常、Web 版式、大纲、打印布局、打印预览）和 [!INCLUDE[TLA#tla_wmp](../../../includes/tlasharptla-wmp-md.md)] 外观。  
  
 实现自定义控件类型的控件可以具有表示其功能所需的任何控件模式集。  
  
## 请参阅  
 [UI Automation Control Patterns](../../../docs/framework/ui-automation/ui-automation-control-patterns.md)   
 [UI Automation Text Pattern](../../../docs/framework/ui-automation/ui-automation-text-pattern.md)   
 [Invoke a Control Using UI Automation](../../../docs/framework/ui-automation/invoke-a-control-using-ui-automation.md)   
 [Get the Toggle State of a Check Box Using UI Automation](../../../docs/framework/ui-automation/get-the-toggle-state-of-a-check-box-using-ui-automation.md)   
 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)   
 [TextPattern Insert Text Sample](http://msdn.microsoft.com/zh-cn/67353f93-7ee2-42f2-ab76-5c078cf6ca16)   
 [TextPattern Search and Selection Sample](http://msdn.microsoft.com/zh-cn/0a3bca57-8b72-489d-a57c-da85b7a22c7f)   
 [InvokePattern and ExpandCollapsePattern Menu Item Sample](http://msdn.microsoft.com/zh-cn/b7fa141c-e2d1-4da2-a27f-81a7d1172210)