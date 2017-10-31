---
title: "Implementing the UI Automation Scroll Control Pattern | Microsoft Docs"
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
  - "UI Automation, Scroll control pattern"
  - "control patterns, Scroll"
  - "Scroll control pattern"
ms.assetid: 73d64242-6cbb-424c-92dd-dc69530b7899
caps.latest.revision: 23
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 23
---
# Implementing the UI Automation Scroll Control Pattern
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍了实现 <xref:System.Windows.Automation.Provider.IScrollProvider> 的准则和约定，包括有关事件和属性的信息。 本主题的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.ScrollPattern> 控件模式用于支持充当子对象集合的可滚动容器的控件。 尽管通常需要使用滚动条来支持滚动功能，但该控件并不需要。  
  
 ![无滚动栏的滚动控件。](../../../docs/framework/ui-automation/media/uia-scrollpattern-without-scrollbars.PNG "UIA\_ScrollPattern\_Without\_Scrollbars")  
不使用滚动条的滚动控件示例  
  
 有关实现此控件的控件示例，请参阅 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## 实现准则和约定  
 在实现 Scroll 控件模式时，请注意以下准则和约定：  
  
-   此控件的子级必须实现 <xref:System.Windows.Automation.Provider.IScrollItemProvider>。  
  
-   容器控件的滚动条不支持 <xref:System.Windows.Automation.ScrollPattern> 控件模式。 相反，它们必须支持 <xref:System.Windows.Automation.RangeValuePattern> 控件模式。  
  
-   当以百分比度量滚动时，与滚动刻度相关的所有值或量必须规范化为 0 到 100 的范围。  
  
-   <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> 和 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> 独立于 <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty>。  
  
-   如果 <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> \= `false` 则 <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> 应设置为 100%，且 <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> 应设置为 <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>。 类似，如果 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> \= `false` 则 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> 应设置为 100%，且 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> 应设置为 <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>。 这让 UI 自动化客户端能够在 <xref:System.Windows.Automation.ScrollPattern.SetScrollPercent%2A> 方法内使用这些属性值，并在客户端不涉及滚动的方向被激活时避免。  
  
-   <xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalScrollPercent%2A> 是特定于区域设置。 设置 HorizontalScrollPercent \= 100.0 时，则对于英语等从左到右阅读的语言，必须将控件的滚动位置设置为等于其最右位置。 而对于阿拉伯语等从右到左阅读的语言，设置 HorizontalScrollPercent \= 100.0 时必须将滚动位置设置为最左位置。  
  
<a name="Required_Members_for_IScrollProvider"></a>   
## IScrollProvider 必需的成员  
 实现 <xref:System.Windows.Automation.Provider.IScrollProvider> 需要以下属性和方法。  
  
|必需的成员|成员类型|备注|  
|-----------|----------|--------|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalScrollPercent%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticalScrollPercent%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalViewSize%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticalViewSize%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontallyScrollable%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticallyScrollable%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A>|方法|无|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A>|方法|无|  
  
 没有与此控件模式关联的事件。  
  
<a name="Exceptions"></a>   
## 异常  
 提供程序必须引发以下异常。  
  
|异常类型|条件|  
|----------|--------|  
|<xref:System.ArgumentException>|如果控件仅对于水平或垂直滚动支持 <xref:System.Windows.Automation.ScrollAmount> 值，而传入了 <xref:System.Windows.Automation.ScrollAmount> 值，则 <xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A> 将引发此异常。|  
|<xref:System.ArgumentException>|当传入值无法转换为双精度时，<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> 会引发此异常。|  
|<xref:System.ArgumentOutOfRangeException>|当传入大于 100 或小于 0 的值（\-1 除外，因为它等效于 <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>）时，<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> 会引发此异常。|  
|<xref:System.InvalidOperationException>|当尝试在不支持的方向进行滚动时，<xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A> 和 <xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> 都引发此异常。|  
  
## 请参阅  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)