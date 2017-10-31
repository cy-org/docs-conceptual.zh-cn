---
title: "Menu 样式和模板 | Microsoft Docs"
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
  - "ControlTemplate [WPF], 菜单"
  - "Menu [WPF], 样式和模板"
  - "部件 [WPF], 菜单"
  - "状态 [WPF], 菜单"
  - "样式 [WPF], 菜单"
  - "模板 [WPF], 菜单"
ms.assetid: b89da183-9b87-42c6-ac53-731a42c7b09e
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Menu 样式和模板
本主题介绍 <xref:System.Windows.Controls.Menu> 控件的样式和模板。  您可以修改默认的 <xref:System.Windows.Controls.ControlTemplate>，以便为控件提供一个独特的外观。  有关更多信息，请参见[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)。  
  
## 菜单部件  
 <xref:System.Windows.Controls.Menu> 控件没有任何命名部件。  
  
 在为 <xref:System.Windows.Controls.Menu> 创建 <xref:System.Windows.Controls.ControlTemplate> 时，模板可能在 <xref:System.Windows.Controls.ScrollViewer> 中包含 <xref:System.Windows.Controls.ItemsPresenter>。  （<xref:System.Windows.Controls.ItemsPresenter> 显示 <xref:System.Windows.Controls.Menu> 中的每一项；通过 <xref:System.Windows.Controls.ScrollViewer> 可以在控件内滚动）。  如果 <xref:System.Windows.Controls.ItemsPresenter> 不是 <xref:System.Windows.Controls.ScrollViewer> 的直接子级，则您必须为 <xref:System.Windows.Controls.ItemsPresenter> 提供名称 `ItemsPresenter`。  
  
## 菜单状态  
 下表列出了 <xref:System.Windows.Controls.Menu> 控件的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## MenuItem 部件  
 下表列出了 <xref:System.Windows.Controls.Menu> 控件的命名部件。  
  
||||  
|-|-|-|  
|组成部分|类型|说明|  
|PART\_Popup|<xref:System.Windows.Controls.Primitives.Popup>|子菜单的区域。|  
  
 在为 <xref:System.Windows.Controls.MenuItem> 创建 <xref:System.Windows.Controls.ControlTemplate> 时，模板可能在 <xref:System.Windows.Controls.ScrollViewer> 中包含 <xref:System.Windows.Controls.ItemsPresenter>。  （<xref:System.Windows.Controls.ItemsPresenter> 显示 <xref:System.Windows.Controls.MenuItem> 中的每一项；通过 <xref:System.Windows.Controls.ScrollViewer> 可以在控件内滚动）。  如果 <xref:System.Windows.Controls.ItemsPresenter> 不是 <xref:System.Windows.Controls.ScrollViewer> 的直接子级，则您必须为 <xref:System.Windows.Controls.ItemsPresenter> 提供名称 `ItemsPresenter`。  
  
## MenuItem 状态  
 下表列出了 <xref:System.Windows.Controls.MenuItem> 控件的可视状态。  
  
||||  
|-|-|-|  
|VisualState 名称|VisualStateGroup 名称|说明|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## 菜单和 MenuItem ControlTemplate 示例  
 下面的示例演示如何为 <xref:System.Windows.Controls.Menu> 控件定义 <xref:System.Windows.Controls.ControlTemplate>。  
  
 [!code-xml[ControlTemplateExamples#Menu](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#menu)]  
  
 下面的示例演示如何为 <xref:System.Windows.Controls.MenuItem> 控件定义 <xref:System.Windows.Controls.ControlTemplate>。  
  
 [!code-xml[ControlTemplateExamples#MenuItem](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#menuitem)]  
  
 下面的示例定义在前一个示例中使用 `MenuScrollViewer`。  
  
 [!code-xml[ControlTemplateExamples#MenuScrollViewer](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#menuscrollviewer)]  
  
 <xref:System.Windows.Controls.ControlTemplate> 示例使用下面的一个或多个资源。  
  
 [!code-xml[ControlTemplateExamples#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 有关完整示例，请参见 [Styling with ControlTemplates Sample](http://go.microsoft.com/fwlink/?LinkID=160041)（使用 ControlTemplates 设置样式的示例）。  
  
## 请参阅  
 <xref:System.Windows.FrameworkElement.Style%2A>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [Control 样式和模板](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)   
 [控件自定义](../../../../docs/framework/wpf/controls/control-customization.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)