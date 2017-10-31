---
title: "Implementing the UI Automation SelectionItem Control Pattern | Microsoft Docs"
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
  - "Selection Item control pattern"
  - "UI Automation, Selection Item control pattern"
  - "control patterns, Selection Item"
ms.assetid: 76b0949a-5b23-4cfc-84cc-154f713e2e12
caps.latest.revision: 22
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 22
---
# Implementing the UI Automation SelectionItem Control Pattern
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍实现 <xref:System.Windows.Automation.Provider.ISelectionItemProvider> 的准则和约定，包括有关属性、方法和事件的信息。 本概述的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.SelectionItemPattern> 控件模式用于支持充当实现 <xref:System.Windows.Automation.Provider.ISelectionProvider> 的容器控件的独立可选子项的控件。 有关实现此 SelectionItem 控件模式的控件的示例，请参阅 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## 实现准则和约定  
 在实现 Selection Item 控件模式时，请注意以下准则和约定：  
  
-   管理实现 <xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot> 的子控件的单选控件（如“显示属性”对话框中的“屏幕分辨率”滑块）应实现 <xref:System.Windows.Automation.Provider.ISelectionProvider>，且其子级应实现 <xref:System.Windows.Automation.Provider.IRawElementProviderFragment> 和 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>。  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>   
## ISelectionItemProvider 必需的成员  
 以下属性、方法和事件都是实现 <xref:System.Windows.Automation.Provider.ISelectionItemProvider> 所必需的。  
  
|必需的成员|成员类型|备注|  
|-----------|----------|--------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.GetSelection%2A>|方法|无|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|Event|在容器中的选项发生重大更改并需要发送多于 <xref:System.Windows.Automation.Provider.AutomationInteropProvider.InvalidateLimit> 常量所允许的 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent> 和 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent> 事件时引发。|  
  
-   如果 <xref:System.Windows.Automation.SelectionItemPattern.Select%2A>、<xref:System.Windows.Automation.SelectionItemPattern.AddToSelection%2A>或 <xref:System.Windows.Automation.SelectionItemPattern.RemoveFromSelection%2A> 的结果是单个的选定的项，则应引发 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>；否则根据需要发送 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>\/ <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>。  
  
<a name="Exceptions"></a>   
## 异常  
 提供程序必须引发以下异常。  
  
|异常类型|条件|  
|----------|--------|  
|<xref:System.InvalidOperationException>|尝试下列任一操作时：<br /><br /> -   针对 <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> \= `true` 的单选容器调用 <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> 并且已选择元素时。<br />-   针对 <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> \= `true` 的多选容器调用 <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> 并且仅选择了一个元素时。<br />-   针对 <xref:System.Windows.Automation.SelectionPattern.CanSelectMultipleProperty> \= `false` 的单选容器调用 <xref:System.Windows.Automation.Provider.ISelectionItemProvider.AddToSelection%2A> 并且已选择另一个元素时。|  
  
## 请参阅  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Implementing the UI Automation Selection Control Pattern](../../../docs/framework/ui-automation/implementing-the-ui-automation-selection-control-pattern.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)   
 [Fragment Provider Sample](http://msdn.microsoft.com/zh-cn/778ef1bc-8610-4bc9-886e-aeff94a8a13e)