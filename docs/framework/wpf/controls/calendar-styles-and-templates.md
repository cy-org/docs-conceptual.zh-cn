---
title: "Calendar 样式和模板 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Calendar [WPF], 样式和模板"
  - "ControlTemplate [WPF], Calendar"
  - "部件 [WPF], Calendar"
  - "状态 [WPF], Calendar"
  - "样式 [WPF], Calendar"
  - "模板 [WPF], Calendar"
ms.assetid: f4fcf046-7a8f-41b8-b5a8-534b64e0345c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Calendar 样式和模板
本主题介绍 <xref:System.Windows.Controls.Calendar> 控件的样式和模板。  您可以修改默认的 <xref:System.Windows.Controls.ControlTemplate>，以便为控件提供一个独特的外观。  有关更多信息，请参见[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)。  
  
## Calendar 部件  
 下表列出了 <xref:System.Windows.Controls.Calendar> 控件的命名部件。  
  
||||  
|-|-|-|  
|组成部分|类型|说明|  
|PART\_CalendarItem|<xref:System.Windows.Controls.Primitives.CalendarItem>|<xref:System.Windows.Controls.Calendar> 上当前显示的月份或年份。|  
|PART\_Root|<xref:System.Windows.Controls.Panel>|包含 <xref:System.Windows.Controls.Primitives.CalendarItem> 的面板。|  
  
## Calendar 状态  
 下表列出了 <xref:System.Windows.Controls.Calendar> 控件的可视状态。  
  
|VisualState 名称|VisualStateGroup 名称|说明|  
|--------------------|-------------------------|--------|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## CalendarItem 部件  
 下表列出了 <xref:System.Windows.Controls.Primitives.CalendarItem> 控件的命名部件。  
  
||||  
|-|-|-|  
|组成部分|类型|说明|  
|PART\_Root|<xref:System.Windows.FrameworkElement>|控件的根。|  
|PART\_PreviousButton|<xref:System.Windows.Controls.Button>|单击该按钮将显示日历的上一页。|  
|PART\_NextButton|<xref:System.Windows.Controls.Button>|单击该按钮将显示日历的下一页。|  
|PART\_HeaderButton|<xref:System.Windows.Controls.Button>|使用该按钮可在月模式、年模式和十年模式之间切换。|  
|PART\_MonthView|<xref:System.Windows.Controls.Grid>|承载月模式的内容。|  
|PART\_YearView|<xref:System.Windows.Controls.Grid>|承载年或十年模式的内容。|  
|PART\_DisabledVisual|<xref:System.Windows.FrameworkElement>|禁用状态的重叠。|  
|DayTitleTemplate|<xref:System.Windows.DataTemplate>|描述可视结构的 <xref:System.Windows.DataTemplate>。|  
  
## CalendarItem 状态  
 下表列出了 <xref:System.Windows.Controls.Primitives.CalendarItem> 控件的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|Disabled|CommonStates|<xref:System.Windows.UIElement.IsEnabled%2A> 属性为 `false` 时日历的状态。|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## CalendarDayButton 部件  
 <xref:System.Windows.Controls.Primitives.CalendarDayButton> 控件没有任何命名部件。  
  
## CalendarDayButton 状态  
 下表列出了 <xref:System.Windows.Controls.Primitives.CalendarDayButton> 控件的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|禁用|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton> 已禁用。|  
|MouseOver|CommonStates|鼠标指针置于 <xref:System.Windows.Controls.Primitives.CalendarDayButton> 上。|  
|Pressed（已按下）|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton> 已按下。|  
|已选定|SelectionStates|按钮被选定。|  
|未选定|SelectionStates|按钮未被选定。|  
|CalendarButtonFocused|CalendarButtonFocusStates|按钮具有焦点。|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|按钮不具有焦点。|  
|Focused|FocusStates|按钮具有焦点。|  
|Unfocused|FocusStates|按钮不具有焦点。|  
|活动|ActiveStates|按钮处于活动状态。|  
|非活动|ActiveStates|按钮处于非活动状态。|  
|RegularDay|DayStates|按钮不表示 <xref:System.DateTime.Today%2A?displayProperty=fullName>。|  
|Today|DayStates|按钮表示 <xref:System.DateTime.Today%2A?displayProperty=fullName>。|  
|NormalDay|BlackoutDayStates|此按钮表示可以选择的日期。|  
|BlackoutDay|BlackoutDayStates|此按钮表示无法选择的日期。|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## CalendarButton 部件  
 <xref:System.Windows.Controls.Primitives.CalendarButton> 控件没有任何命名部件。  
  
## CalendarButton 状态  
 下表列出了 <xref:System.Windows.Controls.Primitives.CalendarButton> 控件的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|禁用|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton> 已禁用。|  
|MouseOver|CommonStates|鼠标指针置于 <xref:System.Windows.Controls.Primitives.CalendarButton> 上。|  
|Pressed（已按下）|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton> 已按下。|  
|已选定|SelectionStates|按钮被选定。|  
|未选定|SelectionStates|按钮未被选定。|  
|CalendarButtonFocused|CalendarButtonFocusStates|按钮具有焦点。|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|按钮不具有焦点。|  
|Focused|FocusStates|按钮具有焦点。|  
|Unfocused|FocusStates|按钮不具有焦点。|  
|活动|ActiveStates|按钮处于活动状态。|  
|非活动|ActiveStates|按钮处于非活动状态。|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## Calendar ControlTemplate 示例  
 下面的示例演示如何为 <xref:System.Windows.Controls.Calendar> 控件及其关联类型定义 <xref:System.Windows.Controls.ControlTemplate>。  
  
 [!code-xml[ControlTemplateExamples#Calendar](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/calendar.xaml#calendar)]  
  
 上面的示例使用下面的一个或多个资源。  
  
 [!code-xml[ControlTemplateExamples#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 有关完整示例，请参见         [Styling with ControlTemplates Sample](http://go.microsoft.com/fwlink/?LinkID=160041)（使用 ControlTemplates 设置样式的示例）.  
  
## 请参阅  
 <xref:System.Windows.FrameworkElement.Style%2A>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [Control 样式和模板](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)   
 [控件自定义](../../../../docs/framework/wpf/controls/control-customization.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)