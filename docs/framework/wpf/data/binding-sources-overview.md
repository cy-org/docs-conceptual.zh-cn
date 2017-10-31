---
title: "绑定源概述 | Microsoft Docs"
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
ms.assetid: 2df2cd11-6aac-4bdf-ab7b-ea5f464cd5ca
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# 绑定源概述
在数据绑定中，[绑定源](GTMT)对象是指您从其获取数据的对象。  本主题讨论可用作绑定源的对象类型。  
  
   
  
<a name="binding_sources"></a>   
## 绑定源类型  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 数据绑定支持以下[绑定源](GTMT)类型：  
  
|绑定源|说明|  
|---------|--------|  
|[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象|您可以绑定到任何[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象的公共属性、子属性以及索引器。  绑定引擎使用 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 反射来获取属性值。  另外，绑定引擎也可以与实现 <xref:System.ComponentModel.ICustomTypeDescriptor> 或注册了 <xref:System.ComponentModel.TypeDescriptionProvider> 的对象一起使用。<br /><br /> 有关如何实现可充当绑定源的类的更多信息，请参见本主题后面的[针对绑定源实现类](#classes)。|  
|动态对象|您可以绑定到对象的可用属性和索引器，该对象实现 <xref:System.Dynamic.IDynamicMetaObjectProvider> 接口。  如果可访问代码中的成员，则可以绑定到该成员。  例如，如果动态对象允许您通过 `someObjet.AProperty` 访问代码中的成员，则可以通过将绑定路径设置为 `AProperty` 来绑定到该成员。|  
|[!INCLUDE[TLA#tla_adonet](../../../../includes/tlasharptla-adonet-md.md)] 对象|可以绑定到 [!INCLUDE[TLA2#tla_adonet](../../../../includes/tla2sharptla-adonet-md.md)] 对象，如 <xref:System.Data.DataTable>。[!INCLUDE[TLA2#tla_adonet](../../../../includes/tla2sharptla-adonet-md.md)] <xref:System.Data.DataView> 实现 <xref:System.ComponentModel.IBindingList> 接口，该接口提供绑定引擎侦听的更改通知。|  
|[!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 对象|您可以绑定到并运行 <xref:System.Xml.XmlNode>、<xref:System.Xml.XmlDocument> 或 <xref:System.Xml.XmlElement> 上的 `XPath` 查询。  访问 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据（标记中的[绑定源](GTMT)）的简便方式是使用 <xref:System.Windows.Data.XmlDataProvider> 对象。  有关更多信息，请参见[使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)。<br /><br /> 通过使用 LINQ to XML，您还可以绑定到 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument>，或者绑定到对这些类型的对象运行查询而得到的结果。  使用 LINQ to XML 访问 XML 数据（标记中的绑定源）的简便方式是使用 <xref:System.Windows.Data.ObjectDataProvider> 对象。  有关更多信息，请参见[绑定到 XDocument、XElement 或 LINQ for XML 查询结果](../../../../docs/framework/wpf/data/how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)。|  
|<xref:System.Windows.DependencyObject> 对象|您可以绑定到任意 <xref:System.Windows.DependencyObject> 的[依赖项属性](GTMT)。  有关示例，请参见[绑定两个控件的属性](../../../../docs/framework/wpf/data/how-to-bind-the-properties-of-two-controls.md)。|  
  
<a name="classes"></a>   
## 针对绑定源实现类  
 您可以创建自己的绑定源。  本节讨论您在实现类来充当绑定源时需要了解的内容。  
  
### 提供更改通知  
 如果您要使用 <xref:System.Windows.Data.BindingMode> 或 <xref:System.Windows.Data.BindingMode> 绑定（因为您希望 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 在绑定源属性发生动态变化时进行更新），则必须实现一个适当的属性更改通知机制。  建议的机制是使 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 或动态类实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口。  有关更多信息，请参见[实现属性更改通知](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md)。  
  
 如果创建不实现 <xref:System.ComponentModel.INotifyPropertyChanged> 的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象，则必须安排您自己的通知系统，确保绑定中使用的数据保持最新。  您可以通过支持需要更改通知的每个属性的 `PropertyChanged` 模式来提供更改通知。  若要支持此模式，请定义每个属性的*属性名称* Changed 事件，其中*属性名称* 是属性的名称。  每次更改属性时都会引发此事件。  
  
 如果绑定源实现了其中一个通知机制，则会自动进行目标更新。  如果绑定源由于某种原因未提供正确的属性更改通知，则可以选择使用 <xref:System.Windows.Data.BindingExpression.UpdateTarget%2A> 方法来显式更新目标属性。  
  
### 其他特征  
 下表提供了需要注意的其他几个要点：  
  
-   如果您要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中创建对象，则类必须使用默认构造函数。  在某些 [!INCLUDE[TLA2#tla_net](../../../../includes/tla2sharptla-net-md.md)] 语言（例如 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)]）中，可能已为您创建默认构造函数。  
  
-   用作绑定源属性的属性必须是类的公共属性。  不能出于绑定目的来访问显式定义的接口属性，也不能访问没有基实现的受保护、私有、内部或虚拟属性。  
  
-   您不能绑定到公共字段。  
  
-   在您的类中声明的属性类型是传递到绑定的类型。  但是，绑定最终使用的类型取决于[绑定目标](GTMT)属性的类型，而不是绑定源属性的类型。  如果类型不同，您可能需要编写一个转换器来处理最初将您的自定义属性传递到绑定的方式。  有关更多信息，请参见 <xref:System.Windows.Data.IValueConverter>。  
  
<a name="objects"></a>   
## 使用整个对象作为绑定源  
 可以将整个对象用作绑定源。  可通过使用 <xref:System.Windows.Data.Binding.Source%2A> 或 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性来指定绑定源，然后提供一个空白绑定声明：`{Binding}`。  这种方法可发挥较大作用的情况包括：要绑定到属于类型字符串的对象；要绑定到具有您关注的多个属性的对象；要绑定到集合对象。  有关绑定到整个集合对象的示例，请参见[对分层数据使用主\-从模式](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)。  
  
 请注意，您可能需要应用自定义逻辑，使数据对您的绑定目标属性有意义。  自定义逻辑的形式可以是自定义转换器（如果默认类型转换不存在）或者 <xref:System.Windows.DataTemplate>。  有关转换器的更多信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)中“数据转换”一节。  有关数据模板的更多信息，请参见[数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)。  
  
<a name="collections"></a>   
## 使用集合对象作为绑定源  
 通常，要用作绑定源的对象是自定义对象的集合。  每个对象都充当重复绑定的一个实例的源。  例如，您可能有一个 `CustomerOrders` 集合，它由 `CustomerOrder` 对象组成，您的应用程序可以循环访问该集合以确定存在多少订单以及每个订单包含的数据。  
  
 可以枚举实现 <xref:System.Collections.IEnumerable> 接口的任何集合。  但是，若要设置动态绑定，以便集合中的插入或删除操作可以自动更新 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，则该集合必须实现 <xref:System.Collections.Specialized.INotifyCollectionChanged> 接口。  此接口公开一个事件，只要基础集合发生更改，就必须引发该事件。  
  
 <xref:System.Collections.ObjectModel.ObservableCollection%601> 类是公开 <xref:System.Collections.Specialized.INotifyCollectionChanged> 接口的数据集合的内置实现。  该集合中的各个数据对象必须满足前面章节中介绍的要求。  有关示例，请参见[创建和绑定到 ObservableCollection](../../../../docs/framework/wpf/data/how-to-create-and-bind-to-an-observablecollection.md)。  在实现自己的集合之前，请先考虑使用 <xref:System.Collections.ObjectModel.ObservableCollection%601> 或一个现有的集合类，如 <xref:System.Collections.Generic.List%601>、<xref:System.Collections.ObjectModel.Collection%601> 和 <xref:System.ComponentModel.BindingList%601> 等。  
  
 WPF 从不直接绑定到集合。  如果您指定集合作为绑定源，则 WPF 实际会绑定到该集合的默认视图。  有关默认视图的信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
 如果有高级方案并且要实现自己的集合，请考虑使用 <xref:System.Collections.IList> 接口。  <xref:System.Collections.IList> 提供可以通过索引逐个访问的对象的非泛型集合，这样可以提高性能。  
  
<a name="permissions"></a>   
## 数据绑定中的权限要求  
 在进行数据绑定时，必须考虑应用程序的信任级别。  下表总结了在完全信任或部分信任级别下执行的应用程序中可以绑定到的属性类型：  
  
|属性类型<br /><br /> （所有访问修饰符）|动态对象属性|动态对象属性|CLR 属性|CLR 属性|依赖项属性|依赖项属性|  
|------------------------|------------|------------|------------|------------|-----------|-----------|  
|**信任级别**|**完全信任**|**部分信任**|**完全信任**|**部分信任**|**完全信任**|**部分信任**|  
|公共类|是|是|是|是|是|是|  
|非公共类|是|否|是|否|是|是|  
  
 下表描述了数据绑定中有关权限要求的要点：  
  
-   对于 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性，只要绑定引擎能够使用反射访问绑定源属性，数据绑定就能进行。  否则，绑定引擎会发出找不到属性的警告，并使用回退值或默认值（如果可用）。  
  
-   您可以绑定到在编译时或运行时定义的动态对象上的属性。  
  
-   始终可以绑定到[依赖项属性](GTMT)。  
  
 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 绑定的权限要求类似。在部分信任沙盒中，如果 <xref:System.Windows.Data.XmlDataProvider> 没有访问指定数据的权限，则它将失败。  
  
 具有匿名类型的对象为内部对象。  只有在以完全信任方式运行时，您才能绑定到匿名类型的属性。  有关匿名类型的更多信息，请参见[匿名类型（C\# 编程指南）](../Topic/Anonymous%20Types%20\(C%23%20Programming%20Guide\).md)或[匿名类型 \(Visual Basic\)](../Topic/Anonymous%20Types%20\(Visual%20Basic\).md) \(Visual Basic\)。  
  
 有关部分信任安全性的更多信息，请参见 [WPF 部分信任安全](../../../../docs/framework/wpf/wpf-partial-trust-security.md)。  
  
## 请参阅  
 <xref:System.Windows.Data.ObjectDataProvider>   
 <xref:System.Windows.Data.XmlDataProvider>   
 [指定绑定源](../../../../docs/framework/wpf/data/how-to-specify-the-binding-source.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)   
 [使用 LINQ to XML 的 WPF 数据绑定概述](../Topic/WPF%20Data%20Binding%20with%20LINQ%20to%20XML%20Overview.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)