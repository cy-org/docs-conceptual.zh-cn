---
title: "如何：使数据可用于 XAML 中的绑定 | Microsoft Docs"
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
  - "绑定数据, 使数据可用于"
  - "Data Binding — 数据绑定, 使数据可用于绑定"
ms.assetid: 7103c2e8-0e31-4a13-bf12-ca382221a8d5
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使数据可用于 XAML 中的绑定
本主题讨论使数据可用于在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中绑定的不同方式，具体使用哪种方式取决于您的应用程序需要。  
  
## 示例  
 如果您具有一个[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象，并希望从 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 绑定到该对象，使该对象可用于绑定的一种方式就是将其定义为资源，并为其赋予 `x:Key`。  在下面的示例中，假设您具有一个字符串属性名为 `PersonName` 的 `Person` 对象。  `Person` 对象是在名为 `SDKSample` 的命名空间中定义的。  
  
 [!code-xml[SimpleBinding#Instantiation](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#instantiation)]  
[!code-xml[SimpleBinding#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#2)]  
  
 然后，您可以绑定到 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的对象，如下例所示。  
  
 [!code-xml[SimpleBinding#BDO1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#bdo1)]  
  
 您也可以使用 <xref:System.Windows.Data.ObjectDataProvider> 类，如下例所示。  
  
 [!code-xml[SimpleBinding#ODPCP](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Page1.xaml#odpcp)]  
  
 您以相同的方式定义绑定：  
  
 [!code-xml[SimpleBinding#BDO1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#bdo1)]  
  
 在此特定示例中，结果是相同的：您具有一个 <xref:System.Windows.Controls.TextBlock>，其文本内容为 `Joe`。  不过，<xref:System.Windows.Data.ObjectDataProvider> 类提供诸如绑定到方法的结果等功能。  如果需要 <xref:System.Windows.Data.ObjectDataProvider> 类提供的功能，您可以选择使用该类。  
  
 不过，如果要绑定到已经创建的对象，则您需要以代码形式设置 `DataContext`，如下例所示。  
  
 [!code-csharp[ADODataSet#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml.cs#1)]
 [!code-vb[ADODataSet#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ADODataSet/VisualBasic/Window1.xaml.vb#1)]  
  
 若要使用 <xref:System.Windows.Data.XmlDataProvider> 类访问用于绑定的 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据，请参见[使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)。  若要使用 <xref:System.Windows.Data.ObjectDataProvider> 类访问用于绑定的 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据，请参见[绑定到 XDocument、XElement 或 LINQ for XML 查询结果](../../../../docs/framework/wpf/data/how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)。  
  
 有关要绑定到的数据的不同指定方式的信息，请参见[指定绑定源](../../../../docs/framework/wpf/data/how-to-specify-the-binding-source.md)。  有关您可以绑定到的数据类型及如何实现自己的[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象以用于绑定的信息，请参见[绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)。  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)