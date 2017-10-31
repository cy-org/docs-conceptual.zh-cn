---
title: "ProgressBar 样式和模板 | Microsoft Docs"
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
  - "ControlTemplate [WPF], ProgressBar"
  - "部件 [WPF], ProgressBar"
  - "ProgressBar [WPF], 样式和模板"
  - "状态 [WPF], ProgressBar"
  - "样式 [WPF], ProgressBar"
  - "模板 [WPF], ProgressBar"
ms.assetid: 935aa600-16e6-4947-a905-37a189a583dd
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# ProgressBar 样式和模板
本主题介绍 <xref:System.Windows.Controls.ProgressBar> 控件的样式和模板。  您可以修改默认的 <xref:System.Windows.Controls.ControlTemplate>，以便为控件提供一个独特的外观。  有关更多信息，请参见[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)。  
  
## ProgressBar 部件  
 下表列出了 <xref:System.Windows.Controls.ProgressBar> 控件的命名部件。  
  
||||  
|-|-|-|  
|组成部分|类型|说明|  
|PART\_Indicator|<xref:System.Windows.FrameworkElement>|指示进度的对象。|  
|PART\_Track|<xref:System.Windows.FrameworkElement>|定义进度指示器的路径的对象。|  
|PART\_GlowRect|<xref:System.Windows.FrameworkElement>|修饰进度栏的对象。|  
  
## ProgressBar 状态  
 下表列出了 <xref:System.Windows.Controls.ProgressBar> 控件的可视状态。  
  
|VisualState 名称|VisualStateGroup 名称|说明|  
|--------------------|-------------------------|--------|  
|Determinate|CommonStates|<xref:System.Windows.Controls.ProgressBar> 基于 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> 属性报告进度。|  
|Indeterminate|CommonStates|<xref:System.Windows.Controls.ProgressBar> 使用重复模式报告泛型进度。|  
|Valid|ValidationStates|该控件使用 <xref:System.Windows.Controls.Validation> 类，<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `false`。|  
|InvalidFocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件具有焦点。|  
|InvalidUnfocused|ValidationStates|当 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 附加属性为 `true` 时，控件没有焦点。|  
  
## ProgressBar ControlTemplate 示例  
 下面的示例演示如何为 <xref:System.Windows.Controls.ProgressBar> 控件定义 <xref:System.Windows.Controls.ControlTemplate>。  
  
 [!code-xml[ControlTemplateExamples#ProgressBar](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/progressbar.xaml#progressbar)]  
  
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