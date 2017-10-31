---
title: "Implementing the UI Automation Value Control Pattern | Microsoft Docs"
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
  - "control patterns, Value"
  - "UI Automation, Value control pattern"
  - "Value control pattern"
ms.assetid: b0fcdd87-3add-4345-bca9-e891205e02ba
caps.latest.revision: 25
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 24
---
# Implementing the UI Automation Value Control Pattern
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍了实现 <xref:System.Windows.Automation.Provider.IValueProvider> 的准则和约定，包括有关事件和属性的信息。 本主题的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.ValuePattern> 控件模式用于支持具有未跨越范围的内部值的控件，以及可用字符串表示的控件。 此字符串是可编辑的，具体取决于控件及其设置。 有关实现此模式的控件的示例，请参阅 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## 实现准则和约定  
 在实现 Value 控件模式时，请注意以下准则和约定：  
  
-   如果任何项的值是可编辑的，则诸如 <xref:System.Windows.Automation.ControlType.ListItem> 和 <xref:System.Windows.Automation.ControlType.TreeItem> 等控件必须支持 <xref:System.Windows.Automation.ValuePattern>，而无论控件的当前编辑模式。 如果子项是可编辑的，则父控件还必须支持 <xref:System.Windows.Automation.ValuePattern>。  
  
 ![可编辑的列表项。](../../../docs/framework/ui-automation/media/uia-valuepattern-editable-listitem.PNG "UIA\_ValuePattern\_Editable\_ListItem")  
可编辑列表项的示例  
  
-   单行编辑控件支持通过实现 <xref:System.Windows.Automation.Provider.IValueProvider> 编程访问其内容。 但是，多行编辑控件不实现 <xref:System.Windows.Automation.Provider.IValueProvider>；相反，它们通过实现 <xref:System.Windows.Automation.Provider.ITextProvider> 来提供对其内容的访问。  
  
-   若要检索多行编辑控件的文本内容，控件必须实现 <xref:System.Windows.Automation.Provider.ITextProvider>。 但是，<xref:System.Windows.Automation.Provider.ITextProvider> 不支持设置控件的值。  
  
-   <xref:System.Windows.Automation.Provider.IValueProvider> 不支持检索格式设置信息或子字符串值。 在这些情况下，请实现 <xref:System.Windows.Automation.Provider.ITextProvider>。  
  
-   <xref:System.Windows.Automation.Provider.IValueProvider> 必须由诸如 [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] 中的“颜色选取器”选择控件（如下所示）之类的控件实现，该控件支持颜色值（例如，“黄色”）与等效的内部 [!INCLUDE[TLA#tla_rgb](../../../includes/tlasharptla-rgb-md.md)] 结构之间的字符串映射。  
  
 ![突出显示黄色的颜色选取器。](../../../docs/framework/ui-automation/media/uia-valuepattern-colorpicker.png "UIA\_ValuePattern\_ColorPicker")  
颜色样本字符串映射的示例  
  
-   在允许调用 <xref:System.Windows.Automation.Provider.IValueProvider.SetValue%2A> 之前，控件应将其 <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty> 设置为 `true`，并将其 <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty> 设置为 `false`。  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>   
## IValueProvider 必需的成员  
 实现 <xref:System.Windows.Automation.Provider.IValueProvider> 需要以下属性和方法。  
  
|必需的成员|成员类型|备注|  
|-----------|----------|--------|  
|<xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty>|属性|无|  
|<xref:System.Windows.Automation.ValuePattern.ValueProperty>|属性|无|  
|<xref:System.Windows.Automation.ValuePattern.SetValue%2A>|方法|无|  
  
<a name="Exceptions"></a>   
## 异常  
 提供程序必须引发以下异常。  
  
|异常类型|条件|  
|----------|--------|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.ValuePattern.SetValue%2A><br /><br /> -   如果向控件传递了格式不正确的区域设置特定信息（如格式不正确的日期）。|  
|<xref:System.ArgumentException>|<xref:System.Windows.Automation.ValuePattern.SetValue%2A><br /><br /> -   如果无法将新值从字符串转换为控件可识别的格式。|  
|<xref:System.Windows.Automation.ElementNotEnabledException>|<xref:System.Windows.Automation.ValuePattern.SetValue%2A><br /><br /> -   当尝试操作未启用的控件时。|  
  
## 请参阅  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [TextPattern Insert Text Sample](http://msdn.microsoft.com/zh-cn/67353f93-7ee2-42f2-ab76-5c078cf6ca16)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)