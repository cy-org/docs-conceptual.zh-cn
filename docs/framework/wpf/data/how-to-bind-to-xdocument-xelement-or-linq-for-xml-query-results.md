---
title: "如何：绑定到 XDocument、XElement 或 LINQ for XML 查询结果 | Microsoft Docs"
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
  - "数据绑定 [WPF], 绑定到 XDocument"
  - "数据绑定 [WPF], 绑定到 XElement"
ms.assetid: 6a629a49-fe1c-465d-b76a-3dcbf4307b64
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# 如何：绑定到 XDocument、XElement 或 LINQ for XML 查询结果
本示例演示如何使用 <xref:System.Xml.Linq.XDocument> 将 XML 数据绑定到 <xref:System.Windows.Controls.ItemsControl>。  
  
## 示例  
 下面的 XAML 代码定义了一个 <xref:System.Windows.Controls.ItemsControl>，并包含了一个用于 `http://planetsNS` XML 命名空间中 `Planet` 类型的数据的数据模板。  占用命名空间的 XML 数据类型必须包含相应的命名空间并用大括号将其括起来，并且，如果它出现在可能出现 XAML 标记扩展的位置，则还必须在相应命名空间前加上大括号转义序列。  此代码绑定到与 <xref:System.Xml.Linq.XElement> 类的 <xref:System.Xml.Linq.XContainer.Element%2A> 和 <xref:System.Xml.Linq.XElement.Attribute%2A> 方法对应的动态属性。  借助动态属性，XAML 可以绑定到共用方法名的动态属性。  若要了解更多信息，请参见 [LINQ to XML 动态属性](../Topic/LINQ%20to%20XML%20Dynamic%20Properties.md)。  请注意 XML 的默认命名空间声明为何不适用于特性名。  
  
 [!code-xml[XLinqExample#StackPanelResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]  
[!code-xml[XLinqExample#ItemsControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#itemscontrol)]  
  
 下面的 C\# 代码调用 <xref:System.Xml.Linq.XDocument.Load%2A> 并将堆叠面板数据上下文设置为 `http://planetsNS` XML 命名空间中名为 `SolarSystemPlanets` 的元素的所有子元素。  
  
 [!code-csharp[XLinqExample#LoadDCFromFile](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromfile)]
 [!code-vb[XLinqExample#LoadDCFromFile](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromfile)]  
  
 可以使用 <xref:System.Windows.Data.ObjectDataProvider> 将 XML 数据存储为 XAML 资源。  有关完整示例，请参见[L2DBForm.xaml 源代码](../Topic/L2DBForm.xaml%20Source%20Code.md)。  下面的示例说明了代码如何将数据上下文设置为对象资源。  
  
 [!code-csharp[XLinqExample#LoadDCFromXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromxaml)]
 [!code-vb[XLinqExample#LoadDCFromXAML](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromxaml)]  
  
 映射到 <xref:System.Xml.Linq.XContainer.Element%2A> 和 <xref:System.Xml.Linq.XElement.Attribute%2A> 的动态属性在 XAML 内提供了灵活性。  代码还可以绑定到 LINQ for XML 查询的结果。  本示例绑定到按元素值排序的查询结果。  
  
 [!code-csharp[XLinqExample#BindToResults](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#bindtoresults)]
 [!code-vb[XLinqExample#BindToResults](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#bindtoresults)]  
  
## 请参阅  
 [绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)   
 [使用 LINQ to XML 的 WPF 数据绑定概述](../Topic/WPF%20Data%20Binding%20with%20LINQ%20to%20XML%20Overview.md)   
 [使用 LINQ to XML 的 WPF 数据绑定示例](../Topic/WPF%20Data%20Binding%20Using%20LINQ%20to%20XML%20Example.md)   
 [LINQ to XML 动态属性](../Topic/LINQ%20to%20XML%20Dynamic%20Properties.md)