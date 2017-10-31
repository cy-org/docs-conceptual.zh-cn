---
title: "如何：转换绑定的数据 | Microsoft Docs"
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
  - "绑定数据, 转换绑定的数据"
  - "转换, 绑定的数据"
  - "Data Binding — 数据绑定, 转换绑定的数据"
ms.assetid: b00aaa19-c6df-4c3b-a9fd-88a0b488df2b
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：转换绑定的数据
本示例演示如何将转换应用于绑定中使用的数据。  
  
 要在绑定期间转换数据，必须创建一个实现 <xref:System.Windows.Data.IValueConverter> 接口的类，其中包括 <xref:System.Windows.Data.IValueConverter.Convert%2A> 和 <xref:System.Windows.Data.IValueConverter.ConvertBack%2A> 方法。  
  
## 示例  
 下面的示例演示一个日期转换器的实现，此日期转换器转换传入的日期值，使其只显示年月日。  实现 <xref:System.Windows.Data.IValueConverter> 接口时，最好用 <xref:System.Windows.Data.ValueConversionAttribute> 特性来修饰此实现，以便向开发工具指示转换所涉及的数据类型，如下面的示例所示：  
  
 [!code-csharp[DataBindingLab#18](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/DateConverter.cs#18)]
 [!code-vb[DataBindingLab#18](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/DateConverter.vb#18)]  
  
 一旦创建了转换器，即可将其作为一项资源添加到[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件中。  在下面的示例中，*src* 映射到在其中定义 *DateConverter* 的命名空间。  
  
 [!code-xml[DataBindingLab#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/DataBindingLabApp.xaml#15)]  
  
 最后，通过以下语法在绑定中使用转换器。  在下面的示例中，<xref:System.Windows.Controls.TextBlock> 的文本内容绑定到 *StartDate*，后者是外部数据源的一个属性。  
  
 [!code-xml[DataBindingLab#17](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/DataBindingLabApp.xaml#17)]  
  
 上述示例中引用的样式资源是在资源部分定义的，该部分未显示在本主题中。  
  
## 请参阅  
 [实现绑定验证](../../../../docs/framework/wpf/data/how-to-implement-binding-validation.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)