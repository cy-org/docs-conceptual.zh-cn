---
title: "Implementing the UI Automation RangeValue Control Pattern | Microsoft Docs"
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
  - "control patterns, Range Value"
  - "Range Value control pattern"
  - "UI Automation, Range Value control pattern"
ms.assetid: 225feaa4-918e-418b-938e-7389338d0a69
caps.latest.revision: 19
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 19
---
# Implementing the UI Automation RangeValue Control Pattern
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍了实现 <xref:System.Windows.Automation.Provider.IRangeValueProvider> 的准则和约定，包括有关事件和属性的信息。 本主题的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.RangeValuePattern> 控件模式用于支持可被设置为范围内的某个值的控件。 有关实现此控件模式的控件示例，请参阅 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## 实现准则和约定  
 在实现 Range Value 控件模式时，请注意以下准则和约定：  
  
-   控件允许基于区域设置或用户首选项来校准支持的属性。 这样的一个示例是温度计控件，它可被设置为以华氏或摄氏显示温度。  
  
-   具有不明确范围值的控件（如进度栏或滑块）应对这些值进行规范化。  
  
 ![进度栏。](../../../docs/framework/ui-automation/media/uia-rangevaluepattern-progress-bar.PNG "UIA\_RangeValuePattern\_Progress\_Bar")  
进度栏的示例，其中值为整数类型，最小和最大属性值分别被规范化为 0 和 100  
  
<a name="Required_Members_for_the_IRangeValueProvider"></a>   
## IRangeValueProvider 必需的成员  
  
|必需的成员|成员类型|备注|  
|-----------|----------|--------|  
|<xref:System.Windows.Automation.RangeValuePattern.IsReadOnlyProperty>|属性|无|  
|<xref:System.Windows.Automation.RangeValuePattern.ValueProperty>|属性|无|  
|<xref:System.Windows.Automation.RangeValuePattern.LargeChangeProperty>|属性|无|  
|<xref:System.Windows.Automation.RangeValuePattern.SmallChangeProperty>|属性|无|  
|<xref:System.Windows.Automation.RangeValuePattern.MaximumProperty>|属性|无|  
|<xref:System.Windows.Automation.RangeValuePattern.MinimumProperty>|属性|无|  
|<xref:System.Windows.Automation.RangeValuePattern.SetValue%2A>|方法|无|  
  
 没有与此控件模式关联的事件。  
  
<a name="Exceptions"></a>   
## 异常  
 提供程序必须引发以下异常。  
  
|异常类型|条件|  
|----------|--------|  
|<xref:System.ArgumentOutOfRangeException>|使用一个大于 <xref:System.Windows.Automation.RangeValuePattern.MaximumProperty> 或小于 <xref:System.Windows.Automation.RangeValuePattern.MinimumProperty> 的值调用 <xref:System.Windows.Automation.RangeValuePattern.SetValue%2A>。|  
  
## 请参阅  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)