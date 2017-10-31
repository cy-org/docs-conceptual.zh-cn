---
title: "标准查询运算符的查询表达式语法 (C#)"
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
ms.assetid: e1e17ef2-68ff-4c26-b6e2-015668227fa5
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
ms.openlocfilehash: 30e994329234b8bd455f739694e50121bac63d5d
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="query-expression-syntax-for-standard-query-operators-c"></a>标准查询运算符的查询表达式语法 (C#)
某些使用更频繁的标准查询运算符具有专用的 C# 语言关键字语法，使用这些语法可以在查询表达式中调用这些运算符。 查询表达式是比基于方法的等效项更具可读性的另一种查询表示形式。 查询表达式子句在编译时被转换为对查询方法的调用。  
  
## <a name="query-expression-syntax-table"></a>查询表达式语法表  
 下表列出包含等效查询表达式子句的标准查询运算符。  
  
|方法|C# 查询表达式语法|  
|------------|---------------------------------|  
|<xref:System.Linq.Enumerable.Cast%2A>|使用显式类型化范围变量，例如：<br /><br /> `from int i in numbers`<br /><br /> （有关详细信息，请参阅 [from 子句](../../../../csharp/language-reference/keywords/from-clause.md)。）|  
|<xref:System.Linq.Enumerable.GroupBy%2A>|`group … by`<br /><br /> - 或 -<br /><br /> `group … by … into …`<br /><br /> （有关详细信息，请参阅 [group 子句](../../../../csharp/language-reference/keywords/group-clause.md)。）|  
|<xref:System.Linq.Enumerable.GroupJoin%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2C%60%603%7D%29>|`join … in … on … equals … into …`<br /><br /> （有关详细信息，请参阅 [join 子句](../../../../csharp/language-reference/keywords/join-clause.md)。）|  
|<xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%29>|`join … in … on … equals …`<br /><br /> （有关详细信息，请参阅 [join 子句](../../../../csharp/language-reference/keywords/join-clause.md)。）|  
|<xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby`<br /><br /> （有关详细信息，请参阅 [orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。）|  
<xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby … descending`<br /><br /> （有关详细信息，请参阅 [orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。）|  
|<xref:System.Linq.Enumerable.Select%2A>|`select`<br /><br /> （有关详细信息，请参阅 [let 子句](../../../../csharp/language-reference/keywords/select-clause.md)。）|  
|<xref:System.Linq.Enumerable.SelectMany%2A>|多个 `from` 子句。<br /><br /> （有关详细信息，请参阅 [from 子句](../../../../csharp/language-reference/keywords/from-clause.md)。）|  
|<xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby …, …`<br /><br /> （有关详细信息，请参阅 [orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。）|  
|<xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby …, … descending`<br /><br /> （有关详细信息，请参阅 [orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。）|  
|<xref:System.Linq.Enumerable.Where%2A>|`where`<br /><br /> （有关详细信息，请参阅 [where 子句](../../../../csharp/language-reference/keywords/where-clause.md)。）|  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq.Enumerable>   
 <xref:System.Linq.Queryable>   
 [标准查询运算符概述 (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [标准查询运算符按执行方式的分类 (C#)](../../../../csharp/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)

