---
title: "UI Automation Support for the RadioButton Control Type | Microsoft Docs"
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
  - "control types, Radio Button"
  - "UI Automation, Radio Button control type"
  - "RadioButton control type"
ms.assetid: 87170464-7857-41f1-bcf7-bb41be31cb53
caps.latest.revision: 21
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 21
---
# UI Automation Support for the RadioButton Control Type
> [!NOTE]
>  本文档适用于想要使用 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md) 命名空间中定义的托管 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 类的 .NET Framework 开发人员。 有关 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 的最新信息，请参阅 Windows 自动化 API：UI 自动化[!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)][!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)][UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)。  
  
 本主题提供有关针对 RadioButton 控件类型的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 支持的信息。 在 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 中，控件类型是一组条件，控件必须满足这些条件才能使用 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md) 属性。 这些条件包括针对 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树结构、[UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md) 属性值和控件模式的特定准则。  
  
 单选按钮包含一个圆形按钮和应用程序定义的文本（标签）、一个图标或者一个表示用户可以通过选择按钮进行选择的位图。 应用程序通常使用分组框中的单选按钮，以允许用户从一组相关，但相互排斥的选项中进行选择。 例如，应用程序可能会提供一组单选按钮，用户可以从中选择一个客户端区域中所选文本的格式首选项。 用户可以通过选择相应的单选按钮来选择左对齐、右对齐或居中的格式。 通常情况下，用户一次只可以从一组单选按钮中选择一项。  
  
 以下几节定义了 RadioButton 控件类型必需的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树结构、属性、控件模式和事件。<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 要求适用于所有列表控件，无论控件是 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)、[!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 还是 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## 必需的 UI 自动化树结构  
 下表描述了与单选按钮控件有关的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树的控件视图和内容视图，以及每个视图中可包含的内容。 有关 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树的详细信息，请参阅 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)。  
  
|控件视图|内容视图|  
|----------|----------|  
|RadioButton|RadioButton|  
  
 控件视图或内容视图中没有子级。  
  
<a name="Required_UI_Automation_Properties"></a>   
## 必需的 UI 自动化属性  
 下表列出了值或定义与 RadioButton 控件类型密切相关的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性。 有关 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性的详细信息，请参阅 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)。  
  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性|值|备注|  
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|--------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|请参阅注释。|此属性的值在应用程序的所有控件中都必须保持唯一。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|请参阅注释。|包含整个控件的最外层矩形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|请参阅注释。|如果该控件可以接收键盘焦点，则它必须支持此属性。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|请参阅注释。|单选按钮控件的名称是保留选定状态的按钮旁显示的文本。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|请参阅注释。|如果用鼠标指针单击，单选按钮控件的可单击点必须是在单选按钮上设置选择的一个点。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|单选按钮为自行进行标记的控件。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|RadioButton|此值对于所有 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 框架均相同。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|“单选按钮”|与 RadioButton 控件类型相对应的本地化字符串。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|单选按钮控件始终包括在 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树的内容视图中。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|单选按钮控件始终包括在 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树的控件视图中。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## 必需的 UI 自动化控件模式  
 下表列出了需要由所有单选按钮控件支持的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 控件模式。 有关控件模式的详细信息，请参阅 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>。  
  
|控件模式\/控件模式属性|支持\/值|备注|  
|------------------|-----------|--------|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|是|所有单选按钮控件必须支持选择项模式才能使其被选。|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider.SelectionContainer%2A>|请参阅注释。|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 必须始终是已完成状态，以便 UI 自动化客户端可以确定特定上下文中还有什么其他的单选按钮关联到另一个按钮。  对于单选按钮的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 版本，不支持此属性，因为无法从旧框架中获取此信息。|  
|<xref:System.Windows.Automation.Provider.IToggleProvider>|Never|单选按钮设置完成之后将无法循环切换其状态。  单选按钮决不能支持此模式。|  
  
<a name="Required_UI_Automation_Events"></a>   
## 必需的 UI 自动化事件  
 下表列出了需要由所有单选按钮控件支持的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 事件。 有关事件的详细信息，请参阅 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>。  
  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 事件|支持|备注|  
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|--------|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|必需|无|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性更改事件。|Never|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性更改事件。|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性更改事件。|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性更改事件。|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必需|无|  
  
## 请参阅  
 <xref:System.Windows.Automation.ControlType.RadioButton>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)