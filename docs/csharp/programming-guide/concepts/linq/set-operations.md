---
title: "集运算 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 7c589367-ef8f-4161-9050-642c47e6bf63
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 121dcd4d41dcfea332c45031a5fbed594e2f1e3e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="set-operations-c"></a>集运算 (C#)
LINQ 中的集运算是指根据相同或不同集合（或集）中是否存在等效元素来生成结果集的查询运算。  
  
 下节列出了执行集运算的标准查询运算符方法。  
  
## <a name="methods"></a>方法  
  
|方法名|描述|C# 查询表达式语法|详细信息|  
|-----------------|-----------------|---------------------------------|----------------------|  
|Distinct|删除集合中的重复值。|不适用。|<xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Distinct%2A?displayProperty=fullName>|  
|Except|返回差集，差集指位于一个集合但不位于另一个集合的元素。|不适用。|<xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Except%2A?displayProperty=fullName>|  
|相交|返回交集，交集指同时出现在两个集合中的元素。|不适用。|<xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Intersect%2A?displayProperty=fullName>|  
|联合|返回并集，并集指位于两个集合中任一集合的唯一的元素。|不适用。|<xref:System.Linq.Enumerable.Union%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Union%2A?displayProperty=fullName>|  
  
## <a name="comparison-of-set-operations"></a>比较集运算  
  
### <a name="distinct"></a>Distinct  
 下图演示字符序列上 <xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName> 方法的行为。 返回的序列包含输入序列的唯一元素。  
  
 ![演示 Distinct&#40;&#41; 的行为的图。](../../../../csharp/programming-guide/concepts/linq/media/distinct.png "Distinct")  
  
### <a name="except"></a>Except  
 下图演示 <xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName> 的行为。 返回的序列只包含位于第一个输入序列但不位于第二个输入序列的元素。  
  
 ![显示 Except&#40;&#41; 的操作的图。](../../../../csharp/programming-guide/concepts/linq/media/except.png "Except")  
  
### <a name="intersect"></a>相交  
 下图演示 <xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName> 的行为。 返回的序列包含两个输入序列共有的元素。  
  
 ![显示两个序列的交集的图。](../../../../csharp/programming-guide/concepts/linq/media/intersect.png "Intersect")  
  
### <a name="union"></a>联合  
 下图演示对两个字符序列执行的联合操作。 返回的序列包含两个输入序列的唯一元素。  
  
 ![显示两个序列的联合的图。](../../../../csharp/programming-guide/concepts/linq/media/union.png "Union")  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq>   
 [标准查询运算符概述 (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [如何：合并和比较字符串集合 (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-combine-and-compare-string-collections-linq.md)   
 [如何：查找两个列表之间的差集 (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-the-set-difference-between-two-lists-linq.md)

