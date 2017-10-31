---
title: "如何：使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据 | Microsoft Docs"
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
  - "绑定, 使用 XmlDataProvider 查询绑定到 XML 数据"
  - "Data Binding — 数据绑定, 使用 XmlDataProvider 查询绑定到 XML 数据"
  - "XmlDataProvider, 绑定到 XML 数据"
ms.assetid: 7dcd018f-16aa-4870-8e47-c1b4ea31e574
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# 如何：使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据
本示例说明如何使用 <xref:System.Windows.Data.XmlDataProvider> 绑定到 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 数据。  
  
 使用 <xref:System.Windows.Data.XmlDataProvider> 时，在应用程序中可通过数据绑定访问的基础数据可以是 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 节点的任意树。  也就是说，<xref:System.Windows.Data.XmlDataProvider> 提供一种将 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 节点的任意树用作[绑定源](GTMT)的简便方式。  
  
## 示例  
 在下面的示例中，数据是作为 <xref:System.Windows.FrameworkElement.Resources%2A> 部分内的 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] *数据岛* 直接嵌入的。  [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据岛必须包装在 `<x:XData>` 标记中，并始终具有一个单一根节点，在本示例中根节点为 *Inventory*。  
  
> [!NOTE]
>  [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据的根节点具有一个将 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 命名空间设置为空字符串的 **xmlns** 特性。  将 XPath 查询应用到 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页中内联的数据岛时，需要此属性。  在此内联情况下，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 以及数据岛会继承 <xref:System.Windows> 命名空间。  因此，您需要将命名空间设置为空白，以防止 XPath 查询被 <xref:System.Windows> 命名空间限定而误导查询。  
  
 [!code-xml[XMLDataSource#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource/CS/Window1.xaml#1)]  
  
 如此示例中所示，若要使用特性语法创建相同的绑定声明，您必须对特殊字符进行正确转义。  有关更多信息，请参见 [XML 字符实体和 XAML](../../../../docs/framework/xaml-services/xml-character-entities-and-xaml.md)。  
  
 运行此示例后，<xref:System.Windows.Controls.ListBox> 将显示下列项。  这些项为 *Books* 下所有元素的 *Title*，其中 *Stock* 值为“*out*”，*Number* 值为 3 或者大于或等于 8。  请注意未返回 *CD* 项，因为在 <xref:System.Windows.Data.XmlDataProvider> 上设置的 <xref:System.Windows.Data.XmlDataProvider.XPath%2A> 值指示应仅公开 *Books* 元素（这是设置筛选器所必需的）。  
  
 ![XPath 示例](../../../../docs/framework/wpf/data/media/xpathexample.png "XPathExample")  
  
 在此示例中，将会显示书名，因为 <xref:System.Windows.DataTemplate> 中 <xref:System.Windows.Controls.TextBlock> 绑定的 <xref:System.Windows.Data.Binding.XPath%2A> 设置为“*Title*”。  如果您希望显示特性值，如 *ISBN*，那么应将 <xref:System.Windows.Data.Binding.XPath%2A> 值设置为“`@ISBN`”。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的 **XPath** 属性是由 XmlNode.SelectNodes 方法处理的。  您可以修改 **XPath** 查询以获取不同的结果。  下面是上述示例中的绑定 <xref:System.Windows.Controls.ListBox> 上的 <xref:System.Windows.Data.Binding.XPath%2A> 查询的一些示例：  
  
-   `XPath="Book[1]"` 将返回第一个 Book 元素（“XML in Action”）。  请注意 **XPath** 索引从 1 而不是从 0 开始。  
  
-   `XPath="Book[@*]"` 将返回带有任意特性的所有 Book 元素。  
  
-   `XPath="Book[last()-1]"` 将返回第二个至最后一个 Book 元素（“Introducing Microsoft .NET”）。  
  
-   `XPath="*[position()>3]"` 将返回除前 3 个元素之外的所有 Book 元素。  
  
 当运行 **XPath** 查询时，它将返回 <xref:System.Xml.XmlNode> 或 XmlNode 列表。  <xref:System.Xml.XmlNode> 是一个[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象，这意味着可以使用 <xref:System.Windows.Data.Binding.Path%2A> 属性绑定到[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性。  再以上述示例为例。  如果该示例的其余部分保持不变，您将 <xref:System.Windows.Controls.TextBlock> 绑定更改为下面的值，那么您将在 <xref:System.Windows.Controls.ListBox> 中看到返回的 XmlNode 的名称。  在此情况下，所有返回节点的名称为“*Book*”。  
  
 [!code-xml[XmlDataSourceVariation#XmlNodePath](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSourceVariation/CS/Page1.xaml#xmlnodepath)]  
  
 在某些应用程序中，将 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 作为 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页的源内的数据岛嵌入可能很不方便，因为在编译时必须知道该数据的确切内容。  因此，还支持从外部 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 文件获取该数据，如下面的示例所示：  
  
 [!code-xml[XMLDataSource2#XmlFileExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource2/CS/Window1.xaml#xmlfileexample)]  
  
 如果 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据驻留在远程 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 文件中，那么可以通过将适当的 [!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)] 分配给 <xref:System.Windows.Data.XmlDataProvider.Source%2A> 特性来定义对该数据的访问，如下所示：  
  
```  
<XmlDataProvider x:Key="BookData" Source="http://MyUrl" XPath="Books"/>  
```  
  
## 请参阅  
 <xref:System.Windows.Data.ObjectDataProvider>   
 [绑定到 XDocument、XElement 或 LINQ for XML 查询结果](../../../../docs/framework/wpf/data/how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)   
 [对分层 XML 数据使用主\-从模式](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)   
 [绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)