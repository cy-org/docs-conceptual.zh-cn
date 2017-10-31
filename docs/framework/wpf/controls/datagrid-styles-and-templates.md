---
title: "DataGrid 样式和模板 | Microsoft Docs"
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
  - "ControlTemplate [WPF], DataGrid"
  - "DataGrid [WPF], 样式和模板"
  - "部件 [WPF], DataGrid"
  - "状态 [WPF], DataGrid"
  - "样式 [WPF], DataGrid"
  - "模板 [WPF], DataGrid"
ms.assetid: 9cb31d63-f148-4d25-b079-816e73f988c7
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# DataGrid 样式和模板
本主题介绍 <xref:System.Windows.Controls.DataGrid> 控件的样式和模板。  您可以修改默认的 <xref:System.Windows.Controls.ControlTemplate>，以便为控件提供一个独特的外观。  有关更多信息，请参见[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)。  
  
## DataGrid 部件  
 下表列出了 <xref:System.Windows.Controls.DataGrid> 控件的命名部件。  
  
||||  
|-|-|-|  
|组成部分|类型|说明|  
|PART\_ColumnHeadersPresenter|<xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter>|包含列标题的行。|  
  
 在为 <xref:System.Windows.Controls.DataGrid> 创建 <xref:System.Windows.Controls.ControlTemplate> 时，模板可能在 <xref:System.Windows.Controls.ScrollViewer> 中包含 <xref:System.Windows.Controls.ItemsPresenter>。  （<xref:System.Windows.Controls.ItemsPresenter> 显示 <xref:System.Windows.Controls.DataGrid> 中的每一项；通过 <xref:System.Windows.Controls.ScrollViewer> 可以在控件内滚动）。  如果 <xref:System.Windows.Controls.ItemsPresenter> 不是 <xref:System.Windows.Controls.ScrollViewer> 的直接子级，则您必须为 <xref:System.Windows.Controls.ItemsPresenter> 提供名称 `ItemsPresenter`。  
  
 <xref:System.Windows.Controls.DataGrid> 的默认模板包含一个 <xref:System.Windows.Controls.ScrollViewer> 控件。  有关由 <xref:System.Windows.Controls.ScrollViewer> 定义的部件的更多信息，请参见 [ScrollViewer 样式和模板](../../../../docs/framework/wpf/controls/scrollviewer-styles-and-templates.md)。  
  
## DataGrid 状态  
 下表列出了 <xref:System.Windows.Controls.DataGrid> 控件的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|禁用|CommonStates|控件被禁用。|  
|InvalidFocused|ValidationStates|控件无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|控件无效并且没有焦点。|  
|Valid|ValidationStates|控件有效。|  
  
## DataGridCell 部件  
 <xref:System.Windows.Controls.DataGridCell> 元素没有任何命名部件。  
  
## DataGridCell 状态  
 下表列出了 <xref:System.Windows.Controls.DataGridCell> 元素的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针置于单元格上。|  
|Focused|FocusStates|单元格具有焦点。|  
|Unfocused|FocusStates|单元格没有焦点|  
|当前|CurrentStates|单元格是当前单元格。|  
|规则|CurrentStates|单元格不是当前单元格。|  
|显示|InteractionStates|单元格处于显示模式。|  
|编辑|InteractionStates|单元格处于编辑模式。|  
|已选定|SelectionStates|单元格已选择。|  
|未选定|SelectionStates|单元格未选择。|  
|InvalidFocused|ValidationStates|单元格无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|单元格无效，并且没有焦点。|  
|Valid|ValidationStates|单元格有效。|  
  
## DataGridRow 部件  
 <xref:System.Windows.Controls.DataGridRow> 元素没有任何命名部件。  
  
## DataGridRow 状态  
 下表列出了 <xref:System.Windows.Controls.DataGridRow> 元素的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针置于行上。|  
|MouseOver\_Editing|CommonStates|鼠标指针置于行上，并且行处于编辑模式。|  
|MouseOver\_Selected|CommonStates|鼠标指针置于行上，并且行已选择。|  
|MouseOver\_Unfocused\_Editing|CommonStates|鼠标指针置于行上，行处于编辑模式，并且没有焦点。|  
|MouseOver\_Unfocused\_Selected|CommonStates|鼠标指针置于行上，行已选择，并且没有焦点。|  
|Normal\_AlternatingRow|CommonStates|行是交替行。|  
|Normal\_Editing|CommonStates|行处于编辑模式。|  
|Normal\_Selected|CommonStates|行已选择。|  
|Unfocused\_Editing|CommonStates|行处于编辑模式，并且没有焦点。|  
|Unfocused\_Selected|CommonStates|行已选择，并且没有焦点。|  
|InvalidFocused|ValidationStates|控件无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|控件无效并且没有焦点。|  
|Valid|ValidationStates|控件有效。|  
  
## DataGridRowHeader 部件  
 下表列出了 <xref:System.Windows.Controls.Primitives.DataGridRowHeader> 元素的命名部件。  
  
||||  
|-|-|-|  
|组成部分|类型|说明|  
|PART\_TopHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用于从顶部调整行标题大小的元素。|  
|PART\_BottomHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用于从底部调整行标题大小的元素。|  
  
## DataGridRowHeader 状态  
 下表列出了 <xref:System.Windows.Controls.Primitives.DataGridRowHeader> 元素的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针置于行上。|  
|MouseOver\_CurrentRow|CommonStates|鼠标指针置于行上，并且行是当前行。|  
|MouseOver\_CurrentRow\_Selected|CommonStates|鼠标指针置于行上，行是当前行并已选择。|  
|MouseOver\_EditingRow|CommonStates|鼠标指针置于行上，并且行处于编辑模式。|  
|MouseOver\_Selected|CommonStates|鼠标指针置于行上，并且行已选择。|  
|MouseOver\_Unfocused\_CurrentRow\_Selected|CommonStates|鼠标指针置于行上，行是当前行并已选择，并且没有焦点。|  
|MouseOver\_Unfocused\_EditingRow|CommonStates|鼠标指针置于行上，行处于编辑模式，并且没有焦点。|  
|MouseOver\_Unfocused\_Selected|CommonStates|鼠标指针置于行上，行已选择，并且没有焦点。|  
|Normal\_CurrentRow|CommonStates|行是当前行。|  
|Normal\_CurrentRow\_Selected|CommonStates|行是当前行并已选择。|  
|Normal\_EditingRow|CommonStates|行处于编辑模式。|  
|Normal\_Selected|CommonStates|行已选择。|  
|Unfocused\_CurrentRow\_Selected|CommonStates|行是当前行，已选择，并且没有焦点。|  
|Unfocused\_EditingRow|CommonStates|行处于编辑模式，并且没有焦点。|  
|Unfocused\_Selected|CommonStates|行已选择，并且没有焦点。|  
|InvalidFocused|ValidationStates|控件无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|控件无效并且没有焦点。|  
|Valid|ValidationStates|控件有效。|  
  
## DataGridColumnHeadersPresenter 部件  
 下表列出了 <xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter> 元素的命名部件。  
  
||||  
|-|-|-|  
|组成部分|类型|说明|  
|PART\_FillerColumnHeader|<xref:System.Windows.Controls.Primitives.DataGridColumnHeader>|列标题的占位符。|  
  
## DataGridColumnHeadersPresenter 状态  
 下表列出了 <xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter> 元素的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|InvalidFocused|ValidationStates|单元格无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|单元格无效，并且没有焦点。|  
|Valid|ValidationStates|单元格有效。|  
  
## DataGridColumnHeader 部件  
 下表列出了 <xref:System.Windows.Controls.Primitives.DataGridColumnHeader> 元素的命名部件。  
  
||||  
|-|-|-|  
|组成部分|类型|说明|  
|PART\_LeftHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用于从左侧调整列标题大小的元素。|  
|PART\_RightHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用于从右侧调整列标题大小的元素。|  
  
## DataGridColumnHeader 状态  
 下表列出了 <xref:System.Windows.Controls.Primitives.DataGridColumnHeader> 元素的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针悬停在控件上。|  
|Pressed（已按下）|CommonStates|控件已按下。|  
|SortAscending|SortStates|列按升序排序。|  
|SortDescending|SortStates|列按降序排序。|  
|Unsorted|SortStates|列未排序。|  
|InvalidFocused|ValidationStates|控件无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|控件无效并且没有焦点。|  
|Valid|ValidationStates|控件有效。|  
  
## DataGrid ControlTemplate 示例  
 下面的示例演示如何为 <xref:System.Windows.Controls.DataGrid> 控件及其关联类型定义 <xref:System.Windows.Controls.ControlTemplate>。  
  
 [!code-xml[ControlTemplateExamples#DataGrid](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datagrid.xaml#datagrid)]  
  
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