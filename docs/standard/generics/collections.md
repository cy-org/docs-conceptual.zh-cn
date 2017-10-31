---
title: ".NET Framework 中的泛型集合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "泛型集合 [.NET Framework]"
  - "泛型 [.NET Framework], 集合"
ms.assetid: 5b646751-6ab7-465c-916c-b1a76aefa9f5
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# .NET Framework 中的泛型集合
此主题概述了 .NET Framework 中的泛型集合类和其他泛型类型。  
  
## .NET Framework 中的泛型集合  
 .NET Framework 类库提供了许多 <xref:System.Collections.Generic> 和 <xref:System.Collections.ObjectModel> 命名空间中的泛型集合类。  有关这些类的详细信息，请参阅[常用的集合类型](../../../docs/standard/collections/commonly-used-collection-types.md)。  
  
### System.Collections.Generic  
 许多泛型集合类型均为非泛型类型的直接模拟。  <xref:System.Collections.Generic.Dictionary%602> 是 <xref:System.Collections.Hashtable> 的泛型版本；它使用枚举的泛型结构 <xref:System.Collections.Generic.KeyValuePair%602> 而不是 <xref:System.Collections.DictionaryEntry>。  
  
 <xref:System.Collections.Generic.List%601> 是 <xref:System.Collections.ArrayList> 的泛型版本。  存在响应非泛型版本的泛型 <xref:System.Collections.Generic.Queue%601> 和 <xref:System.Collections.Generic.Stack%601> 类。  
  
 存在 <xref:System.Collections.Generic.SortedList%602> 的泛型和非泛型版本。  这两个版本均为字典和列表的混合。  <xref:System.Collections.Generic.SortedDictionary%602> 泛型类是一个纯字典，并且没有任何非泛型对应项。  
  
 <xref:System.Collections.Generic.LinkedList%601> 泛型类是真正的链接列表。  它没有任何非泛型对应项。  
  
### System.Collections.ObjectModel  
 <xref:System.Collections.ObjectModel.Collection%601> 泛型类提供用于派生自己的泛型集合类型的基类。  <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 类提供了任何从实现 <xref:System.Collections.Generic.IList%601> 泛型接口的类型生成只读集合的简便方法。  <xref:System.Collections.ObjectModel.KeyedCollection%602> 泛型类提供了存储包含其自己的键的对象的方法。  
  
## 其他泛型类型  
 <xref:System.Nullable%601> 泛型结构允许使用值类型，如同它们可分配 `null`。  这在处理数据库查询时很有用，其中字段包含可能丢失的值类型。  泛型类型参数可为任意值类型。  
  
> [!NOTE]
>  在 C\# 中，无需显示使用 <xref:System.Nullable%601>，因为语言具有可以为 null 类型的语法。  
  
 <xref:System.ArraySegment%601> 泛型结构提供了分隔任何类型的从零开始的一维数组内的一系列元素的方法。  泛型类型参数是数组中元素的类型。  
  
 如果你的事件采用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 所使用的事件处理模式，则 <xref:System.EventHandler%601> 泛型委托不需要声明委托类型来处理事件。  例如，假设已创建从 <xref:System.EventArgs> 派生的 `MyEventArgs` 类，以包含事件的数据。  则可以声明此事件，如下所示：  
  
 [!code-cpp[Conceptual.Generics.Overview#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Generics.Overview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source2.cs#7)]
 [!code-vb[Conceptual.Generics.Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source2.vb#7)]  
  
## 请参阅  
 <xref:System.Collections.Generic?displayProperty=fullName>   
 <xref:System.Collections.ObjectModel?displayProperty=fullName>   
 [泛型](../../../docs/standard/generics/index.md)   
 [用于操作数组和列表的泛型委托](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)   
 [泛型接口](../../../docs/standard/generics/interfaces.md)