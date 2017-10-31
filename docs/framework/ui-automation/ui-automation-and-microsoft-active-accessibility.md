---
title: "UI Automation and Microsoft Active Accessibility | Microsoft Docs"
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
  - "Active Accessibility"
  - "UI Automation, Active Accessibility compared to"
  - "UI Automation, Microsoft Active Accessibility"
  - "Active Accessibility, UI Automation compared to"
ms.assetid: 87bee662-0a3e-4232-a421-20e7a5968321
caps.latest.revision: 24
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 23
---
# UI Automation and Microsoft Active Accessibility
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 [!INCLUDE[TLA#tla_aa](../../../includes/tlasharptla-aa-md.md)]是使应用程序具备辅助功能的早期解决方案。[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]是 [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] 的新辅助功能模型，旨在满足对辅助技术产品和自动测试工具的需求。[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]通过 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 提供了很多改进。  
  
 本主题包含了 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的主要功能并解释了这些功能与 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 的不同之处。  
  
<a name="Programming_Languages_compare"></a>   
## 编程语言  
 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]基于 [!INCLUDE[TLA#tla_com](../../../includes/tlasharptla-com-md.md)]，支持双重接口，因此可以用 C\/C\+\+、[!INCLUDE[TLA#tla_vb6](../../../includes/tlasharptla-vb6-md.md)] 和脚本语言进行编程。[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]（包括用于标准控件的客户端提供程序库）用托管代码编写，并且 UI 自动化客户端应用程序可以使用 [!INCLUDE[TLA#tla_vcshrp](../../../includes/tlasharptla-vcshrp-md.md)] 或 [!INCLUDE[TLA#tla_visualbnet](../../../includes/tlasharptla-visualbnet-md.md)] 轻松进行编程。 作为接口实现的 UI 自动化提供程序可以用托管代码或 C\/C\+\+ 编写。  
  
<a name="Support_in_Windows_Presentation_Foundation_"></a>   
## Windows Presentation Foundation 中的支持  
 [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)]是用于创建用户界面的新模型。[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]元素本身不支持 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]；但是，它们支持 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，包括 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 客户端的桥接支持。 只有专门为 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]编写的客户端才可以充分利用 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 的辅助功能，例如对文本的丰富支持。  
  
<a name="Servers_and_Clients_compare"></a>   
## 服务器和客户端  
 在 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]中，服务器和客户端主要通过服务器的 `IAccessible` 实现进行直接通信。  
  
 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中，核心服务位于服务器（称为提供程序）和客户端之间。 核心服务对由提供程序实现的接口进行调用并提供其他服务，例如，为元素生成唯一的运行时标识符。 客户端应用程序使用库函数来调用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]服务。  
  
 UI 自动化提供程序可以将信息提供给 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]客户端，而 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 服务器可以将信息提供给 UI 自动化客户端应用程序。 但是，由于 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]没有公开同 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 一样多的信息，因此两个模型并不完全兼容。  
  
<a name="UI_Elements_compare"></a>   
## UI 元素  
 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]以 `IAccessible` 接口或子标识符的形式呈现 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 元素。 很难比较两个 `IAccessible`指针来确定它们是否引用同一元素。  
  
 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中，每个元素都表示为一个 <xref:System.Windows.Automation.AutomationElement> 对象。 可通过使用相等运算符或 <xref:System.Windows.Automation.AutomationElement.Equals%2A>方法完成比较，这两种方法比较的都是元素的唯一运行时标识符。  
  
<a name="Tree_Views_and_Navigation_compare"></a>   
## 树视图和导航  
 屏幕上的 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)]元素可以被视为树状结构，桌面作为根、应用程序窗口作为直接子项，而应用程序中的元素作为继承子项。  
  
 在 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]中，许多与最终用户不相关的自动化元素都公开在树中。 客户端应用程序需要查看所有元素以确定哪些元素是有意义的。  
  
 UI 自动化客户端应用程序通过筛选视图查看 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]。 该视图仅包含相关元素：向用户提供信息或实现交互的元素。 还提供了只包含控件元素和只包含内容元素的预定义视图；除此之外，应用程序还可以定义自定义视图。[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]简化了向用户描述 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 和帮助用户与应用程序进行交互的任务。  
  
 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]中元素之间的导航可以是空间导航（例如，移动到存在于屏幕左侧的元素）、逻辑导航（例如，移动到下一菜单项或对话框中 Tab 键顺序的下一项）或分层导航（例如，移动到容器中的第一个子级，或者从子级移动到其父级）。 分层导航非常复杂，因为子元素并不总是实现 `IAccessible`的对象。  
  
 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中，所有 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 元素都是支持相同基本功能的 <xref:System.Windows.Automation.AutomationElement> 对象。 （从提供程序的角度来看，它们是实现继承自 <xref:System.Windows.Automation.Provider.IRawElementProviderSimple>的接口的对象。） 导航主要是分层导航：从父级到子级，以及从同级到下一个同级。 （同级之间的导航具有一个逻辑元素，因为它可能遵照的是 Tab 键顺序。） 通过使用 <xref:System.Windows.Automation.TreeWalker>类，你可以使用树的任何筛选视图从任何起点进行导航。 你还可以通过使用 <xref:System.Windows.Automation.AutomationElement.FindFirst%2A>和 <xref:System.Windows.Automation.AutomationElement.FindAll%2A> 导航到特定的子级或继承项；例如，很容易检索对话框中支持指定控件模式的所有元素。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中的导航比 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 中的导航更加一致。 某些元素（例如下拉列表和弹出窗口）在 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]树中出现两次，且从它们进行导航可能出现意外结果。 其实就是无法对 rebar 控件正确实现 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]。[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]能够重排根目录并进行重新布置，因此可以在树的任何位置放置元素，不必考虑窗口所有者构建的层次结构。  
  
<a name="Roles_and_Control_Types"></a>   
## 角色和控件类型  
 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]使用 `accRole` 属性 \(`IAccessible::get_actRole`\) 来检索 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 中元素的角色说明，如 ROLE\_SYSTEM\_SLIDER 或 ROLE\_SYSTEM\_MENUITEM。 元素的角色是确定其可用功能的主要线索。 通过使用固定的方法（如 `IAccessible::accSelect`和 `IAccessible::accDoDefaultAction`）可实现与控件的交互。 客户端应用程序和 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]之间的交互仅限于可通过 `IAccessible` 完成的交互。  
  
 与此相反，[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]很大程度上会将该元素的控件类型（由 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ControlType%2A> 属性描述）从其预期的功能分离。 功能由通过实现其特殊化接口的提供程序支持的控件模式来确定。 可以结合控件模式来描述特定 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]元素支持的完整功能集。 某些提供程序需要支持特定的控件模式；例如，复选框的提供程序必须支持 Toggle 控件模式。 其他提供程序需要支持一个或多个控件模式集；例如，一个按钮必须支持 Toggle 或 Invoke。 还有一些提供程序完全不支持任何控件模式；例如，不能移动、调整大小或停靠的窗格没有任何控件模式。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]支持由 <xref:System.Windows.Automation.ControlType.Custom> 属性标识的自定义控件且可通过 <xref:System.Windows.Automation.AutomationElement.LocalizedControlTypeProperty> 属性描述。  
  
 下表显示了 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]角色到 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 控件类型的映射。  
  
|[!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]角色|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]控件类型|  
|-------------------------------------------------------------------|-------------------------------------------------------------------------------|  
|ROLE\_SYSTEM\_PUSHBUTTON|Button|  
|ROLE\_SYSTEM\_CLIENT|Calendar|  
|ROLE\_SYSTEM\_CHECKBUTTON|复选框|  
|ROLE\_SYSTEM\_COMBOBOX|组合框|  
|ROLE\_SYSTEM\_CLIENT|自定义|  
|ROLE\_SYSTEM\_LIST|数据网格|  
|ROLE\_SYSTEM\_LISTITEM|数据项|  
|ROLE\_SYSTEM\_DOCUMENT|Document|  
|ROLE\_SYSTEM\_TEXT|Edit|  
|ROLE\_SYSTEM\_GROUPING|Group|  
|ROLE\_SYSTEM\_LIST|Header|  
|ROLE\_SYSTEM\_COLUMNHEADER|标头项|  
|ROLE\_SYSTEM\_LINK|超链接|  
|ROLE\_SYSTEM\_GRAPHIC|Image|  
|ROLE\_SYSTEM\_LIST|列表|  
|ROLE\_SYSTEM\_LISTITEM|列表项|  
|ROLE\_SYSTEM\_MENUPOPUP|菜单|  
|ROLE\_SYSTEM\_MENUBAR|菜单栏|  
|ROLE\_SYSTEM\_MENUITEM|Menu item|  
|ROLE\_SYSTEM\_PANE|Pane|  
|ROLE\_SYSTEM\_PROGRESSBAR|进度栏|  
|ROLE\_SYSTEM\_RADIOBUTTON|单选按钮|  
|ROLE\_SYSTEM\_SCROLLBAR|滚动条|  
|ROLE\_SYSTEM\_SEPARATOR|Separator|  
|ROLE\_SYSTEM\_SLIDER|Slider|  
|ROLE\_SYSTEM\_SPINBUTTON|Spinner|  
|ROLE\_SYSTEM\_SPLITBUTTON|“拆分”按钮|  
|ROLE\_SYSTEM\_STATUSBAR|状态栏|  
|ROLE\_SYSTEM\_PAGETABLIST|Tab|  
|ROLE\_SYSTEM\_PAGETAB|选项卡项|  
|ROLE\_SYSTEM\_TABLE|表|  
|ROLE\_SYSTEM\_STATICTEXT|Text|  
|ROLE\_SYSTEM\_INDICATOR|Thumb|  
|ROLE\_SYSTEM\_TITLEBAR|标题栏|  
|ROLE\_SYSTEM\_TOOLBAR|工具栏|  
|ROLE\_SYSTEM\_TOOLTIP|ToolTip|  
|ROLE\_SYSTEM\_OUTLINE|树|  
|ROLE\_SYSTEM\_OUTLINEITEM|树项|  
|ROLE\_SYSTEM\_WINDOW|窗口|  
  
 有关不同控件类型的更多信息，请参阅 [UI Automation Control Types](../../../docs/framework/ui-automation/ui-automation-control-types.md)。  
  
<a name="States_and_Properties"></a>   
## 状态和属性  
 在 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]中，元素支持一组通用的属性集，且某些属性（如 `accState`）必须描述截然不同的事物，具体取决于元素的角色。 服务器必须实现可返回属性的 `IAccessible`的所有方法，返回的属性甚至与该元素不相关。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]可定义更多属性，其中有些属性对应于 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 中的状态。 某些属性是所有元素共有的，但其他属性特定于控件类型和控件模式。 属性由唯一标识符进行区分，并且大多数属性都可通过使用单个方法 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A>或 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A> 进行检索。 许多属性还可以轻松从 <xref:System.Windows.Automation.AutomationElement.Current%2A>和 <xref:System.Windows.Automation.AutomationElement.Cached%2A> 属性访问器进行检索。  
  
 UI 自动化提供程序不需要实现不相关的属性，而可以只返回任何其不支持的属性的 `null`值。 此外，[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]核心服务可以从默认窗口提供程序获取一些属性，并且这些属性与提供程序显式实现的属性相合并。  
  
 除了支持更多属性外，[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]通过允许使用单一跨进程调用检索多个属性来提供更好的性能。  
  
 下表显示了两个模型中属性之间的对应关系。  
  
|[!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]属性访问器|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]属性 ID|备注|  
|----------------------------------------------------------------------|--------------------------------------------------------------------------------|--------|  
|`get_accKeyboardShortcut`|<xref:System.Windows.Automation.AutomationElement.AccessKeyProperty> 或 <xref:System.Windows.Automation.AutomationElement.AcceleratorKeyProperty>|如果两者都存在，`AccessKeyProperty`优先。|  
|`get_accName`|<xref:System.Windows.Automation.AutomationElement.NameProperty>|``|  
|`get_accRole`|<xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>|请参阅上表，了解角色到控件类型的映射。|  
|`get_accValue`|<xref:System.Windows.Automation.ValuePattern.ValueProperty?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.RangeValuePattern.ValueProperty?displayProperty=fullName>|仅对支持 ValuePattern 或 RangeValuePattern 的控件类型有效。 RangeValue 值被规范化为 0\-100，与 MSAA 行为保持一致。 值项使用一个字符串。|  
|`get_accHelp`|<xref:System.Windows.Automation.AutomationElement.HelpTextProperty>||  
|`accLocation`|<xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty>||  
|`get_accDescription`|在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中不受支持|`accDescription`在 MSAA 内没有清晰的规范，这将导致提供程序在此属性中放置不同的信息片段。|  
|`get_accHelpTopic`|在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中不受支持||  
  
 下表显示了哪些 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]属性对应于 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 状态常量。  
  
|[!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]状态|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性|是否触发状态更改？|  
|-------------------------------------------------------------------|------------------------------------------------------------------------------|---------------|  
|STATE\_SYSTEM\_CHECKED|对于复选框，<xref:System.Windows.Automation.TogglePattern.ToggleStateProperty><br /><br /> 对于单选按钮，<xref:System.Windows.Automation.SelectionItemPattern.IsSelectedProperty>|Y|  
|STATE\_SYSTEM\_COLLAPSED|<xref:System.Windows.Automation.ExpandCollapsePattern.ExpandCollapsePatternInformation.ExpandCollapseState%2A> \= <xref:System.Windows.Automation.ExpandCollapseState>|Y|  
|STATE\_SYSTEM\_EXPANDED|<xref:System.Windows.Automation.ExpandCollapsePattern.ExpandCollapsePatternInformation.ExpandCollapseState%2A> \= <xref:System.Windows.Automation.ExpandCollapseState> 或 <xref:System.Windows.Automation.ExpandCollapseState>|Y|  
|STATE\_SYSTEM\_FOCUSABLE|<xref:System.Windows.Automation.AutomationElement.IsKeyboardFocusableProperty>|N|  
|STATE\_SYSTEM\_FOCUSED|<xref:System.Windows.Automation.AutomationElement.HasKeyboardFocusProperty>|N|  
|STATE\_SYSTEM\_HASPOPUP|针对菜单项的 <xref:System.Windows.Automation.ExpandCollapsePattern>|N|  
|STATE\_SYSTEM\_INVISIBLE|<xref:System.Windows.Automation.AutomationElement.IsOffscreenProperty> \= True 且 <xref:System.Windows.Automation.AutomationElement.GetClickablePoint%2A> 导致 <xref:System.Windows.Automation.NoClickablePointException>|N|  
|STATE\_SYSTEM\_LINKED|<xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> \=<br /><br /> <xref:System.Windows.Automation.ControlType.Hyperlink>|N|  
|STATE\_SYSTEM\_MIXED|<xref:System.Windows.Automation.TogglePattern.TogglePatternInformation.ToggleState%2A> \= <xref:System.Windows.Automation.ToggleState>|N|  
|STATE\_SYSTEM\_MOVEABLE|<xref:System.Windows.Automation.TransformPattern.CanMoveProperty>|N|  
|STATE\_SYSTEM\_MUTLISELECTABLE|<xref:System.Windows.Automation.SelectionPattern.CanSelectMultipleProperty>|N|  
|STATE\_SYSTEM\_OFFSCREEN|<xref:System.Windows.Automation.AutomationElement.IsOffscreenProperty> \= True|N|  
|STATE\_SYSTEM\_PROTECTED|<xref:System.Windows.Automation.AutomationElement.IsPasswordProperty>|N|  
|STATE\_SYSTEM\_READONLY|<xref:System.Windows.Automation.RangeValuePattern.IsReadOnlyProperty?displayProperty=fullName> 和 <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty?displayProperty=fullName>|N|  
|STATE\_SYSTEM\_SELECTABLE|支持 <xref:System.Windows.Automation.SelectionItemPattern>|N|  
|STATE\_SYSTEM\_SELECTED|<xref:System.Windows.Automation.SelectionItemPattern.IsSelectedProperty>|N|  
|STATE\_SYSTEM\_SIZEABLE|<xref:System.Windows.Automation.TransformPattern.TransformPatternInformation.CanResize%2A>|N|  
|STATE\_SYSTEM\_UNAVAILABLE|<xref:System.Windows.Automation.AutomationElement.IsEnabledProperty>|Y|  
  
 以下状态或者未由大多数 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]控制服务器实现，或者在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 中没有等效项。  
  
|[!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]状态|备注|  
|-------------------------------------------------------------------|--------|  
|STATE\_SYSTEM\_BUSY|在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中不可用|  
|STATE\_SYSTEM\_DEFAULT|在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中不可用|  
|STATE\_SYSTEM\_ANIMATED|在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中不可用|  
|STATE\_SYSTEM\_EXTSELECTABLE|未通过 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]服务器广泛实现|  
|STATE\_SYSTEM\_MARQUEED|未通过 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]服务器广泛实现|  
|STATE\_SYSTEM\_SELFVOICING|未通过 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]服务器广泛实现|  
|STATE\_SYSTEM\_TRAVERSED|在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中不可用|  
|STATE\_SYSTEM\_ALERT\_HIGH|未通过 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]服务器广泛实现|  
|STATE\_SYSTEM\_ALERT\_MEDIUM|未通过 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]服务器广泛实现|  
|STATE\_SYSTEM\_ALERT\_LOW|未通过 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]服务器广泛实现|  
|STATE\_SYSTEM\_FLOATING|未通过 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]服务器广泛实现|  
|STATE\_SYSTEM\_HOTTRACKED|在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中不可用|  
|STATE\_SYSTEM\_PRESSED|在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中不可用|  
  
 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]属性标识符的完整列表，请参阅 [UI Automation Properties Overview](../../../docs/framework/ui-automation/ui-automation-properties-overview.md)。  
  
<a name="uiautomation_events_compare"></a>   
## 事件  
 不同于 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 中的事件机制，[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中的事件机制不依赖于 Windows 事件路由（使用窗口句柄紧密连接）且不需要客户端应用程序来设置挂钩。 可以对事件订阅进行微调，不仅能订阅特定事件，甚至还能订阅树的特定部分。 通过跟踪所侦听的事件，提供程序也可微调其事件的引发。  
  
 对于客户端来说检索引发事件的元素也很简单，因为这些事件会被直接传递到事件回调。 如果在客户端订阅该事件时，缓存请求处于活动状态，则会自动预提取元素的属性。  
  
 下表显示了 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] WinEvent 和 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件的对应关系。  
  
|WinEvent|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]事件标识符|  
|--------------|--------------------------------------------------------------------------------|  
|EVENT\_OBJECT\_ACCELERATORCHANGE|<xref:System.Windows.Automation.AutomationElement.AcceleratorKeyProperty>属性更改|  
|EVENT\_OBJECT\_CONTENTSCROLLED|相关联的滚动条上的 <xref:System.Windows.Automation.ScrollPattern.VerticalScrollPercentProperty>或 <xref:System.Windows.Automation.ScrollPattern.HorizontalScrollPercentProperty> 属性更改|  
|EVENT\_OBJECT\_CREATE|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT\_OBJECT\_DEFACTIONCHANGE|无等效项|  
|EVENT\_OBJECT\_DESCRIPTIONCHANGE|没有确切的等效项；也许 <xref:System.Windows.Automation.AutomationElement.HelpTextProperty>或 <xref:System.Windows.Automation.AutomationElement.LocalizedControlTypeProperty> 属性更改|  
|EVENT\_OBJECT\_DESTROY|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT\_OBJECT\_FOCUS|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent>|  
|EVENT\_OBJECT\_HELPCHANGE|<xref:System.Windows.Automation.AutomationElement.HelpTextProperty>已更改|  
|EVENT\_OBJECT\_HIDE|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT\_OBJECT\_LOCATIONCHANGE|<xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty>属性更改|  
|EVENT\_OBJECT\_NAMECHANGE|<xref:System.Windows.Automation.AutomationElement.NameProperty>属性更改|  
|EVENT\_OBJECT\_PARENTCHANGE|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT\_OBJECT\_REORDER|在 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)]中使用不一致。 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中没有定义直接对应的事件。|  
|EVENT\_OBJECT\_SELECTION|<xref:System.Windows.Automation.SelectionItemPattern.ElementSelectedEvent>|  
|EVENT\_OBJECT\_SELECTIONADD|<xref:System.Windows.Automation.SelectionItemPattern.ElementAddedToSelectionEvent>|  
|EVENT\_OBJECT\_SELECTIONREMOVE|<xref:System.Windows.Automation.SelectionItemPattern.ElementRemovedFromSelectionEvent>|  
|EVENT\_OBJECT\_SELECTIONWITHIN|无等效项|  
|EVENT\_OBJECT\_SHOW|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT\_OBJECT\_STATECHANGE|各种属性更改事件|  
|EVENT\_OBJECT\_VALUECHANGE|<xref:System.Windows.Automation.RangeValuePattern.ValueProperty?displayProperty=fullName>和 <xref:System.Windows.Automation.ValuePattern.ValueProperty?displayProperty=fullName> 已更改|  
|EVENT\_SYSTEM\_ALERT|无等效项|  
|EVENT\_SYSTEM\_CAPTUREEND|无等效项|  
|EVENT\_SYSTEM\_CAPTURESTART|无等效项|  
|EVENT\_SYSTEM\_CONTEXTHELPEND|无等效项|  
|EVENT\_SYSTEM\_CONTEXTHELPSTART|无等效项|  
|EVENT\_SYSTEM\_DIALOGEND|<xref:System.Windows.Automation.WindowPattern.WindowClosedEvent>|  
|EVENT\_SYSTEM\_DIALOGSTART|<xref:System.Windows.Automation.WindowPattern.WindowOpenedEvent>|  
|EVENT\_SYSTEM\_DRAGDROPEND|无等效项|  
|EVENT\_SYSTEM\_DRAGDROPSTART|无等效项|  
|EVENT\_SYSTEM\_FOREGROUND|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent>|  
|EVENT\_SYSTEM\_MENUEND|<xref:System.Windows.Automation.AutomationElement.MenuClosedEvent>|  
|EVENT\_SYSTEM\_MENUPOPUPEND|<xref:System.Windows.Automation.AutomationElement.MenuClosedEvent>|  
|EVENT\_SYSTEM\_MENUPOPUPSTART|<xref:System.Windows.Automation.AutomationElement.MenuOpenedEvent>|  
|EVENT\_SYSTEM\_MENUSTART|<xref:System.Windows.Automation.AutomationElement.MenuOpenedEvent>|  
|EVENT\_SYSTEM\_MINIMIZEEND|<xref:System.Windows.Automation.WindowPattern.WindowVisualStateProperty>属性更改|  
|EVENT\_SYSTEM\_MINIMIZESTART|<xref:System.Windows.Automation.WindowPattern.WindowVisualStateProperty>属性更改|  
|EVENT\_SYSTEM\_MOVESIZEEND|<xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty>属性更改|  
|EVENT\_SYSTEM\_MOVESIZESTART|<xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty>属性更改|  
|EVENT\_SYSTEM\_SCROLLINGEND|<xref:System.Windows.Automation.ScrollPattern.VerticalScrollPercentProperty>或 <xref:System.Windows.Automation.ScrollPattern.HorizontalScrollPercentProperty> 属性更改|  
|EVENT\_SYSTEM\_SCROLLINGSTART|<xref:System.Windows.Automation.ScrollPattern.VerticalScrollPercentProperty>或 <xref:System.Windows.Automation.ScrollPattern.HorizontalScrollPercentProperty> 属性更改|  
|EVENT\_SYSTEM\_SOUND|无等效项|  
|EVENT\_SYSTEM\_SWITCHEND|没有等效项，但 <xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent>事件表示新的应用程序已收到焦点|  
|EVENT\_SYSTEM\_SWITCHSTART|无等效项|  
|无等效项|<xref:System.Windows.Automation.MultipleViewPattern.CurrentViewProperty>属性更改|  
|无等效项|<xref:System.Windows.Automation.ScrollPattern.HorizontallyScrollableProperty>属性更改|  
|无等效项|<xref:System.Windows.Automation.ScrollPattern.VerticallyScrollableProperty>属性更改|  
|无等效项|<xref:System.Windows.Automation.ScrollPattern.HorizontalScrollPercentProperty>属性更改|  
|无等效项|<xref:System.Windows.Automation.ScrollPattern.VerticalScrollPercentProperty>属性更改|  
|无等效项|<xref:System.Windows.Automation.ScrollPattern.HorizontalViewSizeProperty>属性更改|  
|无等效项|<xref:System.Windows.Automation.ScrollPattern.VerticalViewSizeProperty>属性更改|  
|无等效项|<xref:System.Windows.Automation.TogglePattern.ToggleStateProperty>属性更改|  
|无等效项|<xref:System.Windows.Automation.WindowPattern.WindowVisualStateProperty>属性更改|  
|无等效项|<xref:System.Windows.Automation.AutomationElement.AsyncContentLoadedEvent>事件|  
|无等效项|<xref:System.Windows.Automation.AutomationElement.ToolTipOpenedEvent>|  
  
<a name="Security_compare"></a>   
## 安全性  
 某些 `IAccessible`自定义应用场景需要包装一个基本 `IAccessible` 并对其调用。 这具有安全隐患，因为部分受信任的组件不应为代码路径上的中介。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]模型使提供程序不再需要通过其他提供程序代码调用。[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]核心服务将进行所有必要的聚合。  
  
## 请参阅  
 [UI Automation Fundamentals](../../../docs/framework/ui-automation/index.md)