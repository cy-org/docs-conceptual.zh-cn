---
title: "函数编程与过程性编程 (LINQ to XML) (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: ea1015a5-d4c8-4d79-8e1e-ba17a40a4f39
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
ms.openlocfilehash: 9d5afe31c8c81f4b099853a5e6e274156a1baa7f
ms.lasthandoff: 03/13/2017

---
# <a name="functional-vs-procedural-programming-linq-to-xml-visual-basic"></a>函数编程与过程性编程 (LINQ to XML) (Visual Basic)
XML 应用程序有多种类型：  
  
-   有些应用程序采用源 XML 文档并生成与源文档形状不同的新 XML 文档。  
  
-   有些应用程序采用源 XML 文档并生成格式完全不同的结果文档，如 HTML 或 CSV 文本文件。  
  
-   有些应用程序采用源 XML 文档并将记录插入数据库。  
  
-   有些应用程序采用另一个源（如数据库）中的数据并从该数据创建 XML 文档。  
  
 这些并不是所有的 XML 应用程序类型，但它们是 XML 程序员必须实现的一组有代表性的功能类型。  
  
 对于所有这些类型应用程序，开发人员可以采用两种对比方法：  
  
-   使用声明性方法的函数构造。  
  
-   使用过程代码的内存中 XML 树修改法。  
  
 LINQ to XML 同时支持这两种方法。  
  
 使用函数方法时，编写可采用源文档并生成具有所需形状的全新结果文档的转换。  
  
 就地修改 XML 树时，编写可遍历内存中 XML 树节点并在其中导航以便根据需要插入、删除和修改节点的代码。  
  
 可以对任一方法使用 LINQ to XML。 使用的类相同，在某些情况下使用的方法也相同。 但这两种方法的结构和目标却大相径庭。 例如，在不同情况下，其中一种方法通常具有更好的性能，使用更多或更少的内存。 另外，其中一种方法会更容易编写并生成更容易维护的代码。  
  
 若要查看对照这两种方法，请参阅[内存中 XML 树修改与。功能构造 (LINQ to XML) (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/in-memory-xml-tree-modification-vs-functional-construction.md)。  
  
 有关编写函数转换的教程，请参阅[纯功能转换的 XML (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/pure-functional-transformations-of-xml.md)。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to XML 编程概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
