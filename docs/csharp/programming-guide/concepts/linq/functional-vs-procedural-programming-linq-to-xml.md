---
title: "函数编程与过程编程 (LINQ to XML) (C#)"
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
ms.assetid: fc64e39c-a487-4882-9169-da4de97917d9
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
ms.openlocfilehash: 0920206524f9ff93a6be2acdb230f59c244840f7
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="functional-vs-procedural-programming-linq-to-xml-c"></a>函数编程与过程编程 (LINQ to XML) (C#)
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
  
 若要对比查看这两种方法，请参阅[内存中 XML 树修改与函数构造 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml.md)。  
  
 有关编写功能转换的教程，请参阅 [XML 的纯功能转换 (C#)](../../../../csharp/programming-guide/concepts/linq/pure-functional-transformations-of-xml.md)。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to XML 编程概述 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)

