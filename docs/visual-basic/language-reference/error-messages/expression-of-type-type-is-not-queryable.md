---
title: "类型的表达式&lt;类型&gt;不可查询 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc36593
- vbc36593
dev_langs:
- VB
helpviewer_keywords:
- BC36593
ms.assetid: 6f1f5860-bf97-4885-9ebb-bc87d028095c
caps.latest.revision: 5
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1e7e1e2652cf730ef6d14b0579d8a3ee3de67fbb
ms.lasthandoff: 03/13/2017

---
# <a name="expression-of-type-lttypegt-is-not-queryable"></a>类型的表达式&lt;类型&gt;不可查询
类型的表达式\<类型&1;> 不可查询。 请确保没有缺少 LINQ 提供程序程序集引用和/或命名空间导入。  
  
 在中定义的可查询类型<xref:System.Linq>， <xref:System.Data.Linq>，和<xref:System.Xml.Linq>命名空间。</xref:System.Xml.Linq> </xref:System.Data.Linq> </xref:System.Linq> 您必须导入一个或多个这些命名空间，以执行 LINQ 查询。  
  
 <xref:System.Linq>命名空间能让您对查询对象，如集合和数组使用 LINQ。</xref:System.Linq>  
  
 <xref:System.Data.Linq>命名空间能让您可以使用 LINQ 查询 ADO.NET 数据集和 SQL Server 数据库。</xref:System.Data.Linq>  
  
 <xref:System.Xml.Linq>命名空间可用于查询 XML 使用 LINQ 和 Visual Basic 中使用 XML 功能。</xref:System.Xml.Linq>  
  
 **错误 ID:** BC36593  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  添加`Import`语句<xref:System.Linq>， <xref:System.Data.Linq>，或<xref:System.Xml.Linq>到您的代码文件的命名空间。</xref:System.Xml.Linq> </xref:System.Data.Linq> </xref:System.Linq> 您还可以导入的命名空间您的项目使用**引用**项目设计器的页面 (**我的项目**)。  
  
2.  请确保已标识为您的查询的源是可查询类型的类型。 也就是说，实现<xref:System.Collections.Generic.IEnumerable%601>或<xref:System.Linq.IQueryable%601>.</xref:System.Linq.IQueryable%601></xref:System.Collections.Generic.IEnumerable%601>的类型  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq></xref:System.Linq>   
 <xref:System.Data.Linq></xref:System.Data.Linq>   
 <xref:System.Xml.Linq>   
 [在 Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [项目设计器 ->“引用”页 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)
