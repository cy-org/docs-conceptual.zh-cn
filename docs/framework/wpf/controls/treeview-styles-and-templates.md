---
title: "TreeView 样式和模板 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ControlTemplate [WPF], TreeView"
  - "部件 [WPF], TreeView"
  - "状态 [WPF], TreeView"
  - "样式 [WPF], TreeView"
  - "模板 [WPF], TreeView"
  - "TreeView [WPF], 样式和模板"
ms.assetid: a49adb77-0202-4caa-b94a-8bb110d7fa9a
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# TreeView 样式和模板
本主题介绍 <xref:System.Windows.Controls.TreeView> 控件的样式和模板。  您可以修改默认的 <xref:System.Windows.Controls.ControlTemplate>，以便为控件提供一个独特的外观。  有关更多信息，请参见[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)。  
  
## TreeView 部件  
 <xref:System.Windows.Controls.TreeView> 控件没有任何命名部件。  
  
 在为 <xref:System.Windows.Controls.TreeView> 创建 <xref:System.Windows.Controls.ControlTemplate> 时，模板可能在 <xref:System.Windows.Controls.ScrollViewer> 中包含 <xref:System.Windows.Controls.ItemsPresenter>。  （<xref:System.Windows.Controls.ItemsPresenter> 显示 <xref:System.Windows.Controls.TreeView> 中的每一项；通过 <xref:System.Windows.Controls.ScrollViewer> 可以在控件内滚动）。  如果 <xref:System.Windows.Controls.ItemsPresenter> 不是 <xref:System.Windows.Controls.ScrollViewer> 的直接子级，则您必须为 <xref:System.Windows.Controls.ItemsPresenter> 提供名称 `ItemsPresenter`。  
  
## TreeView 状态  
 下表列出了 <xref:System.Windows.Controls.TreeView> 控件的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## TreeViewItem 部件  
 下表列出了 <xref:System.Windows.Controls.TreeViewItem> 控件的命名部件。  
  
|组成部分|类型|说明|  
|----------|--------|--------|  
|PART\_Header|<xref:System.Windows.FrameworkElement>|一个包含 <xref:System.Windows.Controls.TreeView> 控件的标头内容的可视元素。|  
  
## TreeViewItem 状态  
 下表列出了 <xref:System.Windows.Controls.TreeViewItem> 控件的可视状态。  
  
|VisualState 名称|VisualStateGroup 名称|说明|  
|--------------------|-------------------------|--------|  
|Normal|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针置于 <xref:System.Windows.Controls.TreeViewItem> 上。|  
|禁用|CommonStates|<xref:System.Windows.Controls.TreeViewItem> 已禁用。|  
|Focused|FocusStates|<xref:System.Windows.Controls.TreeViewItem> 具有焦点。|  
|Unfocused|FocusStates|<xref:System.Windows.Controls.TreeViewItem> 没有焦点。|  
|展开|ExpansionStates|<xref:System.Windows.Controls.TreeViewItem> 控件已展开。|  
|Collapsed|ExpansionStates|<xref:System.Windows.Controls.TreeViewItem> 控件已折叠。|  
|HasItems|HasItemsStates|<xref:System.Windows.Controls.TreeViewItem> 具有项。|  
|NoItems|HasItemsStates|<xref:System.Windows.Controls.TreeViewItem> 没有项。|  
|已选定|SelectionStates|<xref:System.Windows.Controls.TreeViewItem> 已选定。|  
|SelectedInactive|SelectionStates|<xref:System.Windows.Controls.TreeViewItem> 已选定但不处于活动状态。|  
|未选定|SelectionStates|<xref:System.Windows.Controls.TreeViewItem> 未选定。|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## TreeView ControlTemplate 示例  
 下面的示例演示如何为 <xref:System.Windows.Controls.TreeView> 控件及其关联类型定义 <xref:System.Windows.Controls.ControlTemplate>。  
  
 [!code-xml[ControlTemplateExamples#TreeView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/treeview.xaml#treeview)]  
  
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