---
title: "ComboBox 样式和模板 | Microsoft Docs"
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
  - "ComboBox [WPF], 样式和模板"
  - "ControlTemplate [WPF], 组合框"
  - "部件 [WPF], 组合框"
  - "状态 [WPF], 组合框"
  - "样式 [WPF], 组合框"
  - "模板 [WPF], 组合框"
ms.assetid: b0662fa1-16d7-4320-b26b-c1804e565a44
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# ComboBox 样式和模板
本主题介绍 <xref:System.Windows.Controls.ComboBox> 控件的样式和模板。  您可以修改默认的 <xref:System.Windows.Controls.ControlTemplate>，以便为控件提供一个独特的外观。  有关更多信息，请参见[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)。  
  
## ComboBox 部件  
 下表列出了 <xref:System.Windows.Controls.ComboBox> 控件的命名部件。  
  
||||  
|-|-|-|  
|组成部分|类型|说明|  
|PART\_EditableTextBox|<xref:System.Windows.Controls.TextBox>|包含 <xref:System.Windows.Controls.ComboBox> 的文本。|  
|PART\_Popup|<xref:System.Windows.Controls.Primitives.Popup>|包含组合框中的项的下拉列表。|  
  
 在为 <xref:System.Windows.Controls.ComboBox> 创建 <xref:System.Windows.Controls.ControlTemplate> 时，模板可能在 <xref:System.Windows.Controls.ScrollViewer> 中包含 <xref:System.Windows.Controls.ItemsPresenter>。  （<xref:System.Windows.Controls.ItemsPresenter> 显示 <xref:System.Windows.Controls.ComboBox> 中的每一项；通过 <xref:System.Windows.Controls.ScrollViewer> 可以在控件内滚动）。  如果 <xref:System.Windows.Controls.ItemsPresenter> 不是 <xref:System.Windows.Controls.ScrollViewer> 的直接子级，则您必须为 <xref:System.Windows.Controls.ItemsPresenter> 提供名称 `ItemsPresenter`。  
  
## ComboBox 状态  
 下表列出了 <xref:System.Windows.Controls.ComboBox> 控件的状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|禁用|CommonStates|控件被禁用。|  
|MouseOver|CommonStates|鼠标指针位于 <xref:System.Windows.Controls.ComboBox> 控件上方。|  
|Focused|FocusStates|控件具有焦点。|  
|Unfocused|FocusStates|控件不具有焦点。|  
|FocusedDropDown|FocusStates|<xref:System.Windows.Controls.ComboBox> 的下拉列表具有焦点。|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
|可编辑|EditStates|<xref:System.Windows.Controls.ComboBox.IsEditable%2A> 属性为 `true`。|  
|不可编辑|EditStates|<xref:System.Windows.Controls.ComboBox.IsEditable%2A> 属性为 `false`。|  
  
## ComboBoxItem 部件  
 <xref:System.Windows.Controls.ComboBoxItem> 控件没有任何命名部件。  
  
## ComboBoxItem 状态  
 下表列出了 <xref:System.Windows.Controls.ComboBoxItem> 控件的状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Normal|CommonStates|默认状态。|  
|禁用|CommonStates|控件被禁用。|  
|MouseOver|CommonStates|鼠标指针位于 <xref:System.Windows.Controls.ComboBox> 控件上方。|  
|Focused|FocusStates|控件具有焦点。|  
|Unfocused|FocusStates|控件不具有焦点。|  
|已选定|SelectionStates|该项当前被选定。|  
|未选定|SelectionStates|该项未被选定。|  
|SelectedUnfocused|SelectionStates|该项被选定，但没有焦点。|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## ComboBox ControlTemplate 示例  
 下面的示例演示如何为 <xref:System.Windows.Controls.ComboBox> 控件及其关联类型定义 <xref:System.Windows.Controls.ControlTemplate>。  
  
 [!code-xml[ControlTemplateExamples#ComboBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/combobox.xaml#combobox)]  
  
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