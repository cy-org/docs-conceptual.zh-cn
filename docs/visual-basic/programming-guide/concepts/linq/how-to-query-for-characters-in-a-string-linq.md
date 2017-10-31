---
title: "如何︰ 查询 (LINQ) (Visual Basic 中) 的字符串中的字符 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 499ebbe0-746c-4235-9dba-ce722c12b50e
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dabd63e52707f3078c6cdc41db8c4f0e7dfbf70e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-characters-in-a-string-linq-visual-basic"></a>如何︰ 查询 (LINQ) (Visual Basic 中) 的字符串中的字符
因为<xref:System.String>类实现泛型<xref:System.Collections.Generic.IEnumerable%601>接口，可以为字符序列的查询的任何字符串。</xref:System.Collections.Generic.IEnumerable%601> </xref:System.String> 但是，这不是 LINQ 的一个常见用途。 对于复杂的模式匹配操作中，使用<xref:System.Text.RegularExpressions.Regex>类。</xref:System.Text.RegularExpressions.Regex>  
  
## <a name="example"></a>示例  
 下面的示例查询字符串以确定它包含的数字位数。 请注意，该查询"重用"后它会在执行第一次。 这可能是因为查询本身不存储任何实际的结果。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## <a name="compiling-the-code"></a>编译代码  
 创建一个面向.NET Framework 版本 3.5 或更高版本对 System.Core.dll 的引用与项目和一个`Imports`System.Linq 命名空间的语句。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ 和字符串 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)   
 [如何︰ 将 LINQ 查询与正则表达式 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-combine-linq-queries-with-regular-expressions.md)
