---
title: "如何：从已绑定的目标属性获取绑定对象 | Microsoft Docs"
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
  - "Data Binding — 数据绑定, 从绑定目标属性获取绑定对象"
  - "属性, 获取绑定对象"
ms.assetid: 87974c5f-136b-4de7-b07d-9285b62ab123
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：从已绑定的目标属性获取绑定对象
此示例演示如何从数据绑定目标属性获取绑定对象。  
  
## 示例  
 您可以执行以下操作以获取 <xref:System.Windows.Data.Binding> 对象：  
  
 [!code-csharp[BindValidation#GetBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml.cs#getbinding)]  
  
> [!NOTE]
>  您必须为所需的绑定指定[依赖项属性](GTMT)，因为目标对象的多个属性可能正在使用数据绑定。  
  
 或者，可以获取 <xref:System.Windows.Data.BindingExpression>，然后获取 <xref:System.Windows.Data.BindingExpression.ParentBinding%2A> 属性的值。  
  
 有关完整示例，请参见 [Binding Validation Sample](http://go.microsoft.com/fwlink/?LinkID=159972)（绑定验证示例）。  
  
> [!NOTE]
>  如果您的绑定是 <xref:System.Windows.Data.MultiBinding>，请使用 <xref:System.Windows.Data.BindingOperations>.<xref:System.Windows.Data.BindingOperations.GetMultiBinding%2A>。  如果它是 <xref:System.Windows.Data.PriorityBinding>，请使用 <xref:System.Windows.Data.BindingOperations>.<xref:System.Windows.Data.BindingOperations.GetPriorityBinding%2A>。  如果您不确定目标属性是使用 <xref:System.Windows.Data.Binding>、<xref:System.Windows.Data.MultiBinding> 还是 <xref:System.Windows.Data.PriorityBinding> 绑定的，则可以使用 <xref:System.Windows.Data.BindingOperations>.<xref:System.Windows.Data.BindingOperations.GetBindingBase%2A>。  
  
## 请参阅  
 [在代码中创建绑定](../../../../docs/framework/wpf/data/how-to-create-a-binding-in-code.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)