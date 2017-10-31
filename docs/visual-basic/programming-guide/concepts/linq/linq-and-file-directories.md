---
title: "LINQ 和文件目录 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 159fd5c3-3926-4071-ae78-d8e423287eb7
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5536ae95b42cdaddda2c4cae97a114681e94b0ab
ms.lasthandoff: 03/13/2017

---
# <a name="linq-and-file-directories-visual-basic"></a>LINQ 和文件目录 (Visual Basic)
许多文件系统操作实质上是查询，因此非常适合 LINQ 方法。  
  
 请注意，本部分中的查询非破坏性。 它们不用于更改原始文件或文件夹的内容。 这遵循该规则查询不应引起任何副作用。 一般情况下，修改源数据的任何代码 （包括执行的查询创建 / 更新 / 删除运算符） 应始终独立于只查询数据的代码。  
  
 本节包含下列主题：  
  
 [如何︰ 查询具有指定的特性或名称 (Visual Basic 中) 的文件](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-files-with-a-specified-attribute-or-name.md)  
 演示如何通过检查一个或多个属性文件中搜索其<xref:System.IO.FileInfo>对象。</xref:System.IO.FileInfo>  
  
 [如何︰ 通过扩展 (LINQ) (Visual Basic 中) 的文件进行分组](../../../../visual-basic/programming-guide/concepts/linq/how-to-group-files-by-extension-linq.md)  
 演示如何返回组<xref:System.IO.FileInfo>对象基于其文件扩展名。</xref:System.IO.FileInfo>  
  
 [如何︰ 查询一组文件夹 (LINQ) (Visual Basic 中) 中的字节总数](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders.md)  
 演示如何返回指定的目录树中的所有文件中的总字节数。  
  
 [如何︰ 比较两个文件夹 (LINQ) (Visual Basic 中) 的内容](../../../../visual-basic/programming-guide/concepts/linq/how-to-compare-the-contents-of-two-folders-linq.md)s  
 演示如何返回两个指定的文件夹中存在的所有文件和也的所有文件都位于一个文件夹，但不是在其他。  
  
 [如何︰ 查询多个最大文件或目录树 (LINQ) (Visual Basic 中) 中的文件](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-the-largest-file-or-files-in-a-directory-tree.md)  
 演示如何在目录树中返回的最大或最小的文件或指定的数量的文件。  
  
 [如何︰ 查询目录树 (LINQ) (Visual Basic 中) 中的重复文件](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-duplicate-files-in-a-directory-tree-linq.md)  
 演示如何在指定的目录树中的多个位置中发生的所有文件名称的都组。 此外演示如何执行更复杂的比较基于自定义比较器。  
  
 [如何︰ 查询文件夹 (LINQ) (Visual Basic 中) 中的文件的内容](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-the-contents-of-files-in-a-folder-linq.md)  
 演示如何遍历树中的文件夹，打开每个文件，以及查询文件的内容。  
  
## <a name="comments"></a>注释  
 在创建的数据源，准确地表示文件系统的内容，并能正确处理异常时涉及是某种程度的复杂性。 本部分中的示例创建的快照集合<xref:System.IO.FileInfo>对象，表示指定的根文件夹下的所有文件和所有子文件夹。</xref:System.IO.FileInfo> 实际状态的每个<xref:System.IO.FileInfo>在何时开始和结束执行查询之间的时间可能会更改。</xref:System.IO.FileInfo> 例如，您可以创建一份<xref:System.IO.FileInfo>要用作数据源对象。</xref:System.IO.FileInfo> 如果您尝试访问`Length`属性在查询中，<xref:System.IO.FileInfo>对象将尝试访问文件系统来更新的值`Length`。</xref:System.IO.FileInfo> 如果该文件不再存在，则会出现<xref:System.IO.FileNotFoundException>在查询中，即使您不文件系统直接查询。</xref:System.IO.FileNotFoundException> 本部分中的某些查询使用一个单独的方法使用在某些情况下这些特定异常。 另一个选项是使您通过使用<xref:System.IO.FileSystemWatcher>。</xref:System.IO.FileSystemWatcher>动态更新的数据源  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
