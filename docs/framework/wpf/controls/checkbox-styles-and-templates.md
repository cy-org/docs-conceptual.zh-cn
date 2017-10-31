---
title: "CheckBox 样式和模板 | Microsoft Docs"
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
  - "CheckBox [WPF], 样式和模板"
  - "ControlTemplate [WPF], CheckBox"
  - "部件 [WPF], CheckBox"
  - "状态 [WPF], CheckBox"
  - "样式 [WPF], CheckBox"
  - "模板 [WPF], CheckBox"
ms.assetid: bfdaec96-d101-4d3d-864d-c27e6b621d03
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# CheckBox 样式和模板
本主题介绍 <xref:System.Windows.Controls.CheckBox> 控件的样式和模板。  您可以修改默认的 <xref:System.Windows.Controls.ControlTemplate>，以便为控件提供一个独特的外观。  有关更多信息，请参见[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)。  
  
## CheckBox 部件  
 <xref:System.Windows.Controls.CheckBox> 控件没有任何命名的部件。  
  
## CheckBox 状态  
 下表列出了 <xref:System.Windows.Controls.CheckBox> 控件的可视状态。  
  
|VisualState 名称|VisualStateGroup 名称|说明|  
|--------------------|-------------------------|--------|  
|Normal|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针悬停在控件上。|  
|Pressed（已按下）|CommonStates|控件已按下。|  
|禁用|CommonStates|控件被禁用。|  
|Focused|FocusStates|控件具有焦点。|  
|Unfocused|FocusStates|控件不具有焦点。|  
|已选中|CheckStates|<xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> 为 `true`。|  
|未选中|CheckStates|<xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> 为 `false`。|  
|Indeterminate|CheckStates|<xref:System.Windows.Controls.Primitives.ToggleButton.IsThreeState%2A> 为 `true` 且 <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> 为 `null`。|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## CheckBox ControlTemplate 示例  
 下面的示例演示如何为 <xref:System.Windows.Controls.CheckBox> 控件定义 <xref:System.Windows.Controls.ControlTemplate>。  
  
 [!code-xml[ControlTemplateExamples#CheckBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/checkbox.xaml#checkbox)]  
  
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