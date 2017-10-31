---
title: "UI Automation Support for the Table Control Type | Microsoft Docs"
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
  - "TableControl type"
  - "control types, Table"
  - "UI Automation, Table control type"
ms.assetid: 9050dde5-6469-4c83-abb7-f861c24ff985
caps.latest.revision: 21
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 21
---
# UI Automation Support for the Table Control Type
> [!NOTE]
>  本文档适用于想要使用 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md) 命名空间中定义的托管 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 类的 .NET Framework 开发人员。 有关 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 的最新信息，请参阅 Windows 自动化 API：UI 自动化[!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)][!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)][UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)。  
  
 本主题提供了 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 对于 Table 控件类型的支持信息。 在 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 中，控件类型是一组条件，控件必须满足这些条件才能使用 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md) 属性。 这些条件包括针对 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树结构、[UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md) 属性值和控件模式的特定准则。  
  
 Table 控件包含文本的行和列和（可选）行标头和列标头。  
  
 以下几节定义了 Table 控件类型必需的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树结构、属性、控件模式和事件。<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 要求适用于所有 Table 控件，无论控件是 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)、[!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 还是 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## 必需的 UI 自动化树结构  
 下表描述了与 Table 控件有关的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树的控件视图和内容视图，以及每个视图中可包含的内容。 有关 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 树的详细信息，请参阅 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)。  
  
|控件视图|内容视图|  
|----------|----------|  
|表<br /><br /> -   标头（0 个或 1 个）<br />-   Text（0 个或 1 个）<br />-   各种控件（0 个或多个）|表<br /><br /> -   Text（0 个或多个）<br />-   各种控件（0 个或多个）|  
  
 如果 Table 控件具有标题行或列标头，则它们必须在 UI 自动化树的控件视图中公开。 内容视图不需要公开此信息，因为可以使用 TablePattern 进行访问。  
  
<a name="Required_UI_Automation_Properties"></a>   
## 必需的 UI 自动化属性  
 下表列出了 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性，这些属性的值或定义与 Table 控件尤其相关。 有关 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性的详细信息，请参阅 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)。  
  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性|值|备注|  
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|--------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|请参阅注释。|此属性的值在应用程序的所有控件中都必须保持唯一。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|请参阅注释。|包含整个控件的最外层矩形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|请参阅注释。|如果存在边界矩形，则受支持。 如果边界矩形中存在无法单击的点，而你要执行专门的命中测试，则重写并提供可单击的点。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|请参阅注释。|如果该控件可以接收键盘焦点，则它必须支持此属性。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|请参阅注释。|Table 控件通常从静态文本标签中获取其名称。 如果没有静态文本标签，必须分配一个 Name 属性，该属性必须始终可用，以说明表的用途。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|请参阅注释。|如果没有静态文本标签，则此属性应公开对该控件的自动化元素的引用。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|表|此值对于所有 UI 框架均相同。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|“表”|与 Table 控件类型相对应的已本地化字符串。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|请参阅注释。|如果未通过访问 NameProperty 进行充分解释，应通过此属性公开更多有关表的用途的详细信息。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.DescribedByProperty>|请参阅注释。|如果该表由其他 UI 元素（例如，保存对表的说明的文本元素）进行了批注，则 DescribedBy 属性应公开对文本控件的自动化元素的引用。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Table 控件必须始终包含内容。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Table 控件必须始终为一个控件。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## 必需的 UI 自动化控件模式  
 下表列出了需要由 Table 控件支持的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 控件模式。 有关控件模式的详细信息，请参阅 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>。  
  
|控件模式|支持|备注|  
|----------|--------|--------|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|是|Table 控件始终支持此控件模式，因为它包含的项具有在网格中显示的数据。|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider>|是（需要子对象）|一个表的内部对象应支持的 GridItem 和 TableItem 控件模式。 表本身不需要支持 GridItem 或 TableItem 控件模式，除非该表是另一个表的一部分。|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|是|Table 控件始终具备拥有与内容相关的标头的能力。|  
|<xref:System.Windows.Automation.Provider.ITableItemProvider>|是（需要子对象）|一个表的内部对象应支持的 GridItem 和 TableItem 控件模式。 表本身不需要支持 GridItem 或 TableItem 控件模式，除非该表是另一个表的一部分。|  
  
<a name="Required_UI_Automation_Events"></a>   
## 必需的 UI 自动化事件  
 下表列出了需要由所有 Table 控件支持的 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 事件。 有关事件的详细信息，请参阅 <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>。  
  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 事件|支持|备注|  
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|--------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性更改事件。|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性更改事件。|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性更改事件。|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必需|无|  
  
## 请参阅  
 <xref:System.Windows.Automation.ControlType.Table>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)