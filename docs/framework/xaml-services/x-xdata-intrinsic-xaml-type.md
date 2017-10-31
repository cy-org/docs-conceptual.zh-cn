---
title: "x:XData Intrinsic XAML Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "x:XData"
  - "XData"
  - "xXData"
helpviewer_keywords: 
  - "XAML [XAML Services], x:XData directive element"
  - "XData in XAML [XAML Services]"
  - "x:XData XAML directive element [XAML Services]"
ms.assetid: 7ce209c2-621b-4977-b643-565f7e663534
caps.latest.revision: 17
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 17
---
# x:XData Intrinsic XAML Type
在 XAML 生产中开启 XML 数据岛的放置。  `x:XData` 中的 XML 元素不应由 XAML 处理器处理，就像它们属于作用的默认 XAML 命名空间或任何其他 XAML 命名空间的一部分。  `x:XData` 可包含任意格式正确的 XML。  
  
## XAML 对象元素用法  
  
```  
<x:XData>  
  <elementDataRoot>  
    [elementData]  
  </elementDataRoot>  
</x:XData>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`elementDataRoot`|封闭的数据岛的单个根元素。  对于大多数最终使用者，没有单个根的 XML 被认为无效。  尤其是，如果 `x:XData` 旨在作为 WPF 或将 XML 源用于数据绑定的许多其他技术的 XML 数据源，则需要一个根。|  
|`[elementData]`|可选。  表示 XML 数据的 XML。  但是，可以包含任意数目的元素作为元素数据和嵌套元素可以包含在其他元素中应用 XML 的通用规则。|  
  
## 备注  
 `x:XData` 对象中的 XML 元素可以重新声明数据内包含的 XMLDOM 的所有可能的命名空间和前缀。  
  
 通过 <xref:System.Windows.Markup.XData> 类，对 XML 数据和 `x:XData` 内在 XAML 类型的编程访问可能存在于 .NET Framework XAML 服务中。  
  
## WPF 用法说明  
 `x:XData` 对象主要用作 <xref:System.Windows.Data.XmlDataProvider> 的子对象，或者用作 <xref:System.Windows.Data.XmlDataProvider.XmlSerializer%2A?displayProperty=fullName> 属性的子对象（在 XAML 中，通常用属性元素语法表示）。  
  
 通常，数据应将数据岛内的基 XML 命名空间重新定义为新的默认 XML 命名空间（设置为空字符串）。  对于简单数据岛，这是最容易的方法，因为用于引用和绑定到数据的 <xref:System.Windows.Data.Binding.XPath%2A> 表达式可以避免包含前缀。  较为复杂的数据岛可能选择为数据定义多个前缀，并为根级别的 XML 命名空间使用一个特定的前缀。  在此情况下，所有 <xref:System.Windows.Data.Binding.XPath%2A> 表达式引用都应包含相应的命名空间映射前缀。  有关更多信息，请参见[数据绑定概述](../../../ocs/framework/wpf/data/data-binding-overview.md)。  
  
 通常，`x:XData` 可用作 <xref:System.Xml.Serialization.IXmlSerializable> 类型的任何属性的内容。  但是，<xref:System.Windows.Data.XmlDataProvider.XmlSerializer%2A?displayProperty=fullName> 是唯一突出的实现。  
  
## 请参阅  
 <xref:System.Windows.Data.XmlDataProvider>   
 [数据绑定概述](../../../ocs/framework/wpf/data/data-binding-overview.md)   
 [绑定标记扩展](../../../ocs/framework/wpf/advanced/binding-markup-extension.md)