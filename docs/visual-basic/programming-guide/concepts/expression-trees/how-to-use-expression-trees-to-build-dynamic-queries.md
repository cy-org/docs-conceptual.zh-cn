---
title: "如何︰ 使用表达式树来生成动态查询 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 16278787-7532-4b65-98b2-7a412406c4ee
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8d69be78a9f3568535dffe54e21af80c6eb12f70
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-use-expression-trees-to-build-dynamic-queries-visual-basic"></a>如何︰ 使用表达式树来生成动态查询 (Visual Basic)
在 LINQ 中，表达式目录树用于表示该目标的数据源实现<xref:System.Linq.IQueryable%601>。</xref:System.Linq.IQueryable%601>的结构化的查询 例如，LINQ 提供程序实现<xref:System.Linq.IQueryable%601>接口，用于查询关系数据存储区。</xref:System.Linq.IQueryable%601> Visual Basic 编译器编译成代码，将生成一个表达式树，在运行时针对此类数据源的查询。 然后，查询提供程序可以遍历表达式树数据结构，并将其转换为适用于数据源的查询语言。  
  
 表达式树还能用于在 LINQ 中用于表示分配给类型<xref:System.Linq.Expressions.Expression%601>。</xref:System.Linq.Expressions.Expression%601>的变量的 lambda 表达式  
  
 本主题介绍如何使用表达式树来创建动态 LINQ 查询。 在查询的细节在编译时未知时，动态查询很有用。 例如，应用程序可能会提供一个用户界面，使最终用户若要指定一个或多个谓词来筛选的数据。 若要使用 LINQ 进行查询，这种应用程序必须使用表达式树来在运行时创建 LINQ 查询。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用表达式树来构造查询针对`IQueryable`数据源，然后执行它。 代码将生成表达式树来表示以下查询︰  
  
 `companies.Where(Function(company) company.ToLower() = "coho winery" OrElse company.Length > 16).OrderBy(Function(company) company)`  
  
 中的工厂方法<xref:System.Linq.Expressions>命名空间用来创建表达式目录树表示构成总体查询的表达式。</xref:System.Linq.Expressions> 表示对标准查询运算符方法的调用的表达式引用<xref:System.Linq.Queryable>这些方法的实现。</xref:System.Linq.Queryable> 最终的表达式树传递给<xref:System.Linq.IQueryProvider.CreateQuery%60%601%28System.Linq.Expressions.Expression%29>的提供程序实现`IQueryable`数据源，以创建类型的可执行查询`IQueryable`。</xref:System.Linq.IQueryProvider.CreateQuery%60%601%28System.Linq.Expressions.Expression%29> 可通过枚举该查询变量获取结果。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 此代码传递给该谓词中使用固定的数量的表达式`Queryable.Where`方法。 但是，您可以编写合并可变数量的谓词表达式依赖于用户输入的应用程序。 此外可以使用不同的标准查询运算符的调用在查询中，具体取决于用户的输入。  
  
## <a name="compiling-the-code"></a>编译代码  
  
-   创建一个新**控制台应用程序**项目。  
  
-   如果未引用将添加对 System.Core.dll 的引用。  
  
-   包括 System.Linq.Expressions 命名空间。  
  
-   从该示例复制代码并将其粘贴到`Main``Sub`过程。  
  
## <a name="see-also"></a>另请参阅  
 [表达式树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)   
 [如何︰ 执行表达式树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)
