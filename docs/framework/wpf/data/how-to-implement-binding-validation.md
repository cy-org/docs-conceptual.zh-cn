---
title: "如何：实现绑定验证 | Microsoft Docs"
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
  - "绑定, 验证"
  - "Data Binding — 数据绑定, 绑定验证"
  - "绑定验证"
ms.assetid: eb98b33d-9866-49ae-b981-bc5ff20d607a
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：实现绑定验证
此示例演示如何基于自定义的验证规则，使用 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> 和样式触发器来提供可视反馈，以便在输入无效值时向用户发出通知。  
  
## 示例  
 下面示例中的 <xref:System.Windows.Controls.TextBox> 的文本内容绑定到名为 `ods` 的[绑定源](GTMT)对象的 `Age` 属性（类型为 int）。  该绑定设置用于使用名为 `AgeRangeRule` 的验证规则，以便当用户输入了非数值字符或输入的值小于 21 或者大于 130 时，文本框旁边将显示一个红色感叹号，并且当用户将鼠标移动到该文本框上时，将显示包含错误消息的工具提示。  
  
 [!code-xml[BindValidation#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#2)]  
  
 下面的示例演示了 `AgeRangeRule` 的实现，该实现从 <xref:System.Windows.Controls.ValidationRule> 继承并重写 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法。  对值调用 Int32.Parse\(\) 方法，以确保该值不包含任何无效字符。  <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法返回 <xref:System.Windows.Controls.ValidationResult>，该结果基于分析期间是否引发了异常以及生存期值是否超出了上界和下界，来指示该值是否有效。  
  
 [!code-csharp[BindValidation#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/AgeRangeRule.cs#3)]  
  
 下面的示例演示了自定义的 <xref:System.Windows.Controls.ControlTemplate> `validationTemplate`，它用于创建一个红色感叹号，以通知用户验证错误。  控件模板用于重新定义控件的外观。  
  
 [!code-xml[BindValidation#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#4)]  
  
 如下面的示例中所示，显示错误消息的 <xref:System.Windows.Controls.ToolTip> 是使用名为 `textBoxInError` 的样式创建的。  如果 <xref:System.Windows.Controls.Validation.HasError%2A> 的值是 `true`，则触发器将当前 <xref:System.Windows.Controls.TextBox> 的工具提示设置为其第一个验证错误。  <xref:System.Windows.Data.Binding.RelativeSource%2A> 设置为 <xref:System.Windows.Data.RelativeSourceMode>，以引用当前元素。  
  
 [!code-xml[BindValidation#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#5)]  
  
 有关完整示例，请参见 [Binding Validation Sample](http://go.microsoft.com/fwlink/?LinkID=159972)（绑定验证示例）。  
  
 请注意，如果未提供自定义的 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A>，则当出现验证错误时，将显示默认错误模板来为用户提供可视反馈。  有关更多信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)中的“数据验证”。  另外，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还提供了内置验证规则，该规则捕获在更新绑定源属性期间引发的异常。  有关更多信息，请参见 <xref:System.Windows.Controls.ExceptionValidationRule>。  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)