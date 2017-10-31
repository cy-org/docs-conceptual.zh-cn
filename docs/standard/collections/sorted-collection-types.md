---
title: "已排序的集合类型"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SortedDictionary collection type
- SortedList class, grouping data in collections
- grouping data in collections, SortedList collection type
- SortedList collection type
- collections [.NET Framework], SortedList collection type
ms.assetid: 3db965b2-36a6-4b12-b76e-7f074ff7275a
caps.latest.revision: 16
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 210582c6cf31b59f7f6c4b577c0e8a2c2f25ddd6
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="sorted-collection-types"></a>已排序的集合类型
<xref:System.Collections.SortedList?displayProperty=fullName> 类、<xref:System.Collections.Generic.SortedList%602?displayProperty=fullName> 泛型类和 <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName> 泛型类与 <xref:System.Collections.Hashtable> 类和 <xref:System.Collections.Generic.Dictionary%602> 泛型类的相似之处在于均实现 <xref:System.Collections.IDictionary> 接口，不同之处在于它们让元素一直按键的排序顺序排列，并且不具备哈希表的 O(1) 插入和检索特性。 这三个类具有若干共性：  
  
-   这三个类全都实现 <xref:System.Collections.IDictionary?displayProperty=fullName> 接口。 两个泛型类还实现 <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName> 泛型接口。  
  
-   每个元素都是用于枚举的键/值对。  
  
    > [!NOTE]
    >  枚举时，非泛型 <xref:System.Collections.SortedList> 类返回 <xref:System.Collections.DictionaryEntry> 对象，尽管两个泛型类型返回 <xref:System.Collections.Generic.KeyValuePair%602> 对象。  
  
-   元素按 <xref:System.Collections.IComparer?displayProperty=fullName> 实现代码（对于非泛型 <xref:System.Collections.SortedList>）或 <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName> 实现代码（对于两个泛型类）进行排序。  
  
-   每个类提供了返回仅包含键或仅包含值的集合的属性。  
  
 下表列出了两个已排序列表类与 <xref:System.Collections.Generic.SortedDictionary%602> 类之间的一些区别。  
  
|<xref:System.Collections.SortedList> 非泛型类和 <xref:System.Collections.Generic.SortedList%602> 泛型类|<xref:System.Collections.Generic.SortedDictionary%602> 泛型类|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|返回键和值的属性是有索引的，从而允许高效的索引检索。|无索引的检索。|  
|检索属于 O(log `n`) 操作。|检索属于 O(log `n`) 操作。|  
|插入和删除通常属于 O(`n`) 操作；不过，对于已按排序顺序排列的数据，插入属于 O(log `n`) 操作，这样每个元素都可以添加到列表的末尾。 （这假设不需要调整大小。）|插入和删除属于 O(log `n`) 操作。|  
|比 <xref:System.Collections.Generic.SortedDictionary%602> 使用更少的内存。|比 <xref:System.Collections.SortedList> 非泛型类和 <xref:System.Collections.Generic.SortedList%602> 泛型类使用更多内存。|  
  
 对于必须可通过多个线程并发访问的已排序列表或字典，可以向派生自 <xref:System.Collections.Concurrent.ConcurrentDictionary%602> 的类添加排序逻辑。  
  
> [!NOTE]
>  对于包含自己的键的值（例如，包含雇员 ID 编号的雇员记录），可以通过派生自 <xref:System.Collections.ObjectModel.KeyedCollection%602> 泛型类，创建具有列表和字典的某些特性的键控集合。  
  
 自 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 起，<xref:System.Collections.Generic.SortedSet%601> 类提供在执行插入、删除和搜索操作之后让数据一直按排序顺序排列的自平衡树。 此类和 <xref:System.Collections.Generic.HashSet%601> 类实现 <xref:System.Collections.Generic.ISet%601> 接口。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.IDictionary?displayProperty=fullName>   
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>   
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>   
 [常用的集合类型](../../../docs/standard/collections/commonly-used-collection-types.md)

