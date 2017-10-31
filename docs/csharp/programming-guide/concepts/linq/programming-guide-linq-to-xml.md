---
title: "编程指南 (LINQ to XML) (C#)"
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
ms.assetid: 4b1ffd10-ab81-4a0d-a0ca-e9876478d924
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
ms.openlocfilehash: ed4b0aff72654b9ac0928fae933e34268aede7fe
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="programming-guide-linq-to-xml-c"></a>编程指南 (LINQ to XML) (C#)
本节提供有关使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 进行编程的概念性和指导性信息。  
  
## <a name="who-should-read-this-documentation"></a>本文档的目标读者  
 本文档面向已经了解 C# 以及 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 的一些基本知识的开发人员。  
  
 本文档的目的在于降低各类开发人员对 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的使用难度。 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 使 XML 编程变得更容易。 您无需成为一名专家级开发人员就可以使用它。  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 非常依赖于泛型类。 因此，了解泛型类的使用非常重要。 此外，熟悉作为参数化类型声明的委托也很有帮助。 如果不熟悉 C# 泛型类，请参阅[泛型类](../../../../csharp/programming-guide/generics/generic-classes.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|-----------|-----------------|  
|[LINQ to XML 编程概述 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)|提供对 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 类的概述以及有关以下三个最重要类的详细信息：<xref:System.Xml.Linq.XElement>、<xref:System.Xml.Linq.XAttribute> 和 <xref:System.Xml.Linq.XDocument>。|  
|[创建 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md)|提供有关创建 XML 树的概念性和基于任务的信息。 可以通过使用函数构造，或通过从字符串或文件解析 XML 文本来创建 XML 树。 也可以使用 <xref:System.Xml.XmlReader> 来填充 XML 树。|  
|[使用 XML 命名空间 (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md)|提供有关创建使用命名空间的 XML 树的详细信息。|  
|[序列化 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)|描述序列化 XML 树的多种方法，并给出选择使用方法的指导。|  
|[LINQ to XML 轴 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)|列举并介绍 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 轴方法，您必须了解轴方法才能编写 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查询。|  
|[查询 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/querying-xml-trees.md)|提供查询 XML 树的常见示例。|  
|[修改 XML 树 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)|如同文档对象模型 (DOM) 一样，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 也允许您就地修改 XML 树。|  
|[高级 LINQ to XML 编程 (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)|提供有关批注、事件、流处理和其他高级方案的信息。|  
|[LINQ to XML 安全性 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-security.md)|描述与 LINQ to XML 相关的安全问题并提供减小安全隐患的一些指导。|  
|[示例 XML 文档 (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-documents-linq-to-xml.md)|包含本文档中许多示例使用的示例 XML 文档。|  
  
## <a name="see-also"></a>请参阅  
 [入门 (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/getting-started-linq-to-xml.md)   
 [LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml.md)

