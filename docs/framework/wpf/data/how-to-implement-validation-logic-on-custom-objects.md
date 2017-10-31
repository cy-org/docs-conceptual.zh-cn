---
title: "如何：在自定义对象上实现验证逻辑 | Microsoft Docs"
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
  - "检查验证错误 [WPF]"
  - "自定义对象 [WPF], 实现验证逻辑"
  - "实现自定义对象的验证逻辑 [WPF]"
  - "验证错误 [WPF], 检查"
ms.assetid: 751fda9b-44f9-4d63-b4f2-1df07ac41e0f
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：在自定义对象上实现验证逻辑
本示例演示如何针对自定义对象实现验证逻辑，然后绑定到该对象。  
  
## 示例  
 如果源对象实现了 <xref:System.ComponentModel.IDataErrorInfo>，则可以在业务层提供验证逻辑，如下例所示：  
  
 [!code-csharp[BusinessLayerValidation#IDataErrorInfo](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BusinessLayerValidation/CSharp/Data.cs#idataerrorinfo)]
 [!code-vb[BusinessLayerValidation#IDataErrorInfo](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BusinessLayerValidation/VisualBasic/Data.vb#idataerrorinfo)]  
  
 在下面的示例中，文本框的文本属性绑定到 `Person` 对象的 `Age` 属性，通过 `x:Key` `data` 提供的资源声明，该属性已可用于绑定。  <xref:System.Windows.Controls.DataErrorValidationRule> 检查 <xref:System.ComponentModel.IDataErrorInfo> 实现所引发的验证错误。  
  
 [!code-xml[BusinessLayerValidation#BoundTextBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BusinessLayerValidation/CSharp/Window1.xaml#boundtextbox)]  
  
 如果不使用 <xref:System.Windows.Controls.DataErrorValidationRule>，则可以将 <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> 属性设置为 `true`。  
  
## 请参阅  
 <xref:System.Windows.Controls.ExceptionValidationRule>   
 [实现绑定验证](../../../../docs/framework/wpf/data/how-to-implement-binding-validation.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)