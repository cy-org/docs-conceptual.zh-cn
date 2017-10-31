---
title: "如何：根据绑定项列表生成值 | Microsoft Docs"
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
  - "Data Binding — 数据绑定, 多重绑定"
  - "多重绑定"
ms.assetid: b3d06378-b511-4181-95aa-316d60c9229b
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：根据绑定项列表生成值
使用 <xref:System.Windows.Data.MultiBinding>，您可以将[绑定目标](GTMT)属性绑定到源属性列表，然后应用逻辑以使用给定的输入生成值。  本示例演示如何使用 <xref:System.Windows.Data.MultiBinding>。  
  
## 示例  
 在下面的示例中，`NameListData` 引用包含 `firstName` 和 `lastName` 这两个属性的 `PersonName` 对象的集合。  下面的示例生成一个 <xref:System.Windows.Controls.TextBlock>，以便依次显示人员的姓氏和名字。  
  
 [!code-xml[MultiBinding#Resources1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#resources1)]  
[!code-xml[MultiBinding#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#resources2)]  
[!code-xml[MultiBinding#MultiBindingTextBox2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#multibindingtextbox2)]  
[!code-xml[MultiBinding#Window](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#window)]  
  
 为了了解如何生成姓氏在前的格式，我们来看一看 `NameConverter` 的实现：  
  
 [!code-csharp[MultiBinding#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/NameConverter.cs#3)]
 [!code-vb[MultiBinding#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MultiBinding/VisualBasic/NameConverter.vb#3)]  
  
 `NameConverter` 实现 <xref:System.Windows.Data.IMultiValueConverter> 接口。  `NameConverter` 从各个绑定获取值并将其存储在值对象数组中。  <xref:System.Windows.Data.Binding> 元素在 <xref:System.Windows.Data.MultiBinding> 元素下的显示顺序与它们的值在数组中的存储顺序相同。  <xref:System.Windows.Data.MultiBinding.Converter%2A> 方法的参数引用 <xref:System.Windows.Data.MultiBinding.ConverterParameter%2A> 特性的值，该方法对参数执行转换以确定如何设置名称格式。  
  
## 请参阅  
 [转换绑定的数据](../../../../docs/framework/wpf/data/how-to-convert-bound-data.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)