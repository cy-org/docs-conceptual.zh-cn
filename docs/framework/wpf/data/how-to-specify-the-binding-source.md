---
title: "如何：指定绑定源 | Microsoft Docs"
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
  - "绑定数据, 绑定源"
  - "绑定源"
  - "Data Binding — 数据绑定, Binding Source — 绑定源"
ms.assetid: 55d47757-2648-4a52-987f-b767953f168c
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：指定绑定源
在数据绑定中，[绑定源](GTMT)对象指的是您从其获取数据的对象。  本主题描述了指定[绑定源](GTMT)的几种不同方法。  
  
## 示例  
 如果您要将几个属性绑定到一个通用源，则您需要使用 `DataContext` 属性，它能让您方便地建立一个范围，所有数据绑定的属性都在该范围中继承通用源。  
  
 在下面的示例中，数据上下文建立在应用程序的根元素上。  这允许所有子元素继承该数据上下文。  绑定的数据来自自定义数据类 `NetIncome`，可通过映射直接引用该类，已为该类分配了 `incomeDataSource` 资源键。  
  
 [!code-xml[DirectionalBinding#DataContext1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#datacontext1)]  
[!code-xml[DirectionalBinding#DataContext2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#datacontext2)]  
  
 下面的示例演示 `NetIncome` 类的定义。  
  
 [!code-csharp[DirectionalBinding#DataObject](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/billsdata.cs#dataobject)]
 [!code-vb[DirectionalBinding#DataObject](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DirectionalBinding/VisualBasic/NetIncome.vb#dataobject)]  
  
> [!NOTE]
>  以上示例实例化标记中的对象，并将其用作资源。  如果您希望绑定到已在代码中实例化的对象，则需要通过编程方式设置 `DataContext` 属性。  有关示例，请参见[使数据可用于 XAML 中的绑定](../../../../docs/framework/wpf/data/how-to-make-data-available-for-binding-in-xaml.md)。  
  
 另外，如果您希望在各个绑定上显式指定源，则可以选择以下属性。  这些属性优先于继承的数据上下文。  
  
|属性|说明|  
|--------|--------|  
|<xref:System.Windows.Data.Binding.Source%2A>|可以使用此属性来将源设置为对象的实例。  如果您不需要建立范围（在此范围内若干属性继承同一数据上下文）的功能，您可以使用 <xref:System.Windows.Data.Binding.Source%2A> 属性，而不是 `DataContext` 属性。  有关更多信息，请参见 <xref:System.Windows.Data.Binding.Source%2A>。|  
|<xref:System.Windows.Data.Binding.RelativeSource%2A>|如果您希望指定相对于[绑定目标](GTMT)位置的源，这是有用的。  当您想要将元素的一个属性绑定到同一元素的另一个属性时，或者如果您正在样式或模板中定义绑定，您可能需要使用此属性。  有关更多信息，请参见 <xref:System.Windows.Data.Binding.RelativeSource%2A>。|  
|<xref:System.Windows.Data.Binding.ElementName%2A>|您指定一个表示您希望绑定到的元素的字符串。  当您希望绑定到应用程序中的另一个元素的属性时，这是有用的。  例如，如果您希望使用 <xref:System.Windows.Controls.Slider> 控制应用程序中另一个控件的高度，或者如果您希望将控件的 <xref:System.Windows.Controls.ContentControl.Content%2A> 绑定到 <xref:System.Windows.Controls.ListBox> 控件的 <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> 属性。  有关更多信息，请参见 <xref:System.Windows.Data.Binding.ElementName%2A>。|  
  
## 请参阅  
 <xref:System.Windows.FrameworkElement.DataContext%2A?displayProperty=fullName>   
 <xref:System.Windows.FrameworkContentElement.DataContext%2A?displayProperty=fullName>   
 [属性值继承](../../../../docs/framework/wpf/advanced/property-value-inheritance.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [绑定声明概述](../../../../docs/framework/wpf/data/binding-declarations-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)