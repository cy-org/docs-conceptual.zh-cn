---
title: "LINQ 和字符串 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 75ddb201-d97a-4f98-8cdf-4ad51714529a
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a79d1427331070da9c545fdd3175115fe187e879
ms.lasthandoff: 03/13/2017

---
# <a name="linq-and-strings-visual-basic"></a>LINQ 和字符串 (Visual Basic)
可以使用 LINQ 来查询和转换字符串和字符串集合。 它可以处理文本文件中的半结构化数据尤其有用。 LINQ 查询可以与传统的字符串函数和正则表达式组合。 例如，您可以使用<xref:System.String.Split%2A>或<xref:System.Text.RegularExpressions.Regex.Split%2A>方法来创建一个字符串，然后可以查询或通过使用 LINQ 修改数组。</xref:System.Text.RegularExpressions.Regex.Split%2A> </xref:System.String.Split%2A> 您可以使用<xref:System.Text.RegularExpressions.Regex.IsMatch%2A>中的方法`where`LINQ 查询的子句。</xref:System.Text.RegularExpressions.Regex.IsMatch%2A> 您可以使用 LINQ 查询或修改<xref:System.Text.RegularExpressions.MatchCollection>返回正则表达式的结果。</xref:System.Text.RegularExpressions.MatchCollection>  
  
 本部分中介绍的技术还可用于半结构化的文本数据转换为 XML。 有关详细信息，请参阅[如何︰ 从 CSV 文件生成 XML](how-to-generate-xml-from-csv-files.md)。  
  
 本部分中的示例分为两类︰  
  
## <a name="querying-a-block-of-text"></a>查询文本的块  
 您可以查询、 分析和修改通过使用拆分成较小的字符串的可查询数组的文本块<xref:System.String.Split%2A>方法或<xref:System.Text.RegularExpressions.Regex.Split%2A>方法。</xref:System.Text.RegularExpressions.Regex.Split%2A> </xref:System.String.Split%2A> 可以将源文本拆分为字、 句子、 段落、 页或任何其他条件，并根据他们需要在查询中，然后执行其他拆分。  
  
 [如何︰ 在字符串 (LINQ) (Visual Basic 中) 中单词出现次数进行计数](how-to-count-occurrences-of-a-word-in-a-string-linq.md)  
 演示如何使用 LINQ 进行简单查询文本。  
  
 [如何︰ 查询包含一组指定的字数 (LINQ) (Visual Basic 中) 的句子](how-to-query-for-sentences-that-contain-a-specified-set-of-words.md)

 演示如何将拆分任意边界上的文本文件以及如何针对每个部分执行查询。  
  
 [如何︰ 查询 (LINQ) (Visual Basic 中) 的字符串中的字符](how-to-query-for-characters-in-a-string-linq.md)  
 演示字符串是可查询类型。  
  
 [如何︰ 将 LINQ 查询与正则表达式 (Visual Basic)](how-to-combine-linq-queries-with-regular-expressions.md)  
 演示如何在 LINQ 查询中使用正则表达式，复杂的模式匹配的筛选的查询结果。  
  
## <a name="querying-semi-structured-data-in-text-format"></a>查询以文本格式的半结构化的数据  
 许多不同类型的文本文件包含一系列的行，通常具有类似的格式，如制表符分隔或逗号分隔的文件或固定长度的行。 此类文本文件读入内存之后，可以使用 LINQ 来查询和/或修改的行。 LINQ 查询还简化了组合来自多个源的数据的任务。  
  
 [如何︰ 查找两个列表 (LINQ) (Visual Basic 中) 之间的差集](how-to-find-the-set-difference-between-two-lists-linq.md)  
 演示如何查找位于一个列表，但不是在其他的所有字符串。  
  
 [如何︰ 进行排序或筛选器按任意词或字段 (LINQ) (Visual Basic 中) 的文本数据](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)  
 演示如何基于任意词或字段的文本行进行排序。  
  
 [如何︰ 重新排列带分隔符的文件 (LINQ) (Visual Basic) 字段](how-to-reorder-the-fields-of-a-delimited-file.md)  
 演示如何在.csv 文件中的行中的字段重新排序。  
  
 [如何︰ 组合和比较字符串集合 (LINQ) (Visual Basic)](how-to-combine-and-compare-string-collections-linq.md)  
 演示如何结合使用以各种方式的字符串列表。  
  
 [如何︰ 从多个源 (LINQ) (Visual Basic 中) 填充对象集合](how-to-populate-object-collections-from-multiple-sources-linq.md)  
 演示如何使用多个文本文件作为数据源来创建对象集合。  
  
 [如何︰ 联接不同文件 (LINQ) (Visual Basic 中) 的内容](how-to-join-content-from-dissimilar-files-linq.md)  
 演示如何使用匹配的键将两个列表中的字符串合并成单个字符串。  
  
 [如何︰ 将一个文件拆分成多个文件，通过使用组 (LINQ) (Visual Basic)](how-to-split-a-file-into-many-files-by-using-groups-linq.md)  
 演示如何通过使用同一个文件作为数据源创建新文件。  
  
 [如何︰ 在 CSV 文本文件 (LINQ) (Visual Basic 中) 中计算列值](how-to-compute-column-values-in-a-csv-text-file-linq.md)  
 演示如何以.csv 文件中的文本数据执行数学计算。  
  
## <a name="see-also"></a>另请参阅  
 [语言集成查询 (LINQ) (Visual Basic)](index.md)   
 [如何：从 CSV 文件生成 XML](how-to-generate-xml-from-csv-files.md)

