---
title: "修改 XML 树 (LINQ to XML) (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 4ae511a5-4fc9-4178-9c8e-761357deae3f
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cf605973e68230e9e3e09f0abf6de49635cd5845
ms.lasthandoff: 03/13/2017


---
# <a name="modifying-xml-trees-linq-to-xml-visual-basic"></a>修改 XML 树 (LINQ to XML) (Visual Basic)
[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 是一个 XML 树在内存中的存储区。 加载或解析 XML 树从一个源之后,[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]允许您修改该树中的位置，然后序列化该树，可以将其保存到文件或将其发送到远程服务器。  
  
 当您就地修改树时，可使用某些方法，如<xref:System.Xml.Linq.XContainer.Add%2A>。</xref:System.Xml.Linq.XContainer.Add%2A>  
  
 但是有另外一种方法，就是使用函数构造来生成具有不同形状的新树。 根据需要对 XML 树所做的更改类型的不同，以及根据树大小的不同，该方法可能更加强大，更易于开发。 本节第一个主题将比较这两种方法。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|-----------|-----------------|  
|[内存中 XML 树修改与功能构造 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/in-memory-xml-tree-modification-vs-functional-construction.md)|在内存中修改 XML 树与使用函数构造的比较。|  
|[将元素、 特性和节点添加到 XML 树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/adding-elements-attributes-and-nodes-to-an-xml-tree.md)|提供有关向 XML 树中添加元素、属性或节点的信息。|  
|[修改 XML 树中的元素、特性和节点](../../../../visual-basic/programming-guide/concepts/linq/modifying-elements-attributes-and-nodes-in-an-xml-tree.md)|提供有关修改现有元素、属性或节点的信息。|  
|[从 XML 树 (Visual Basic 中) 中移除元素、 特性和节点](../../../../visual-basic/programming-guide/concepts/linq/removing-elements-attributes-and-nodes-from-an-xml-tree.md)|提供有关从 XML 树中移除元素、属性或节点的信息。|  
|[维护名称/值对 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/maintaining-name-value-pairs.md)|描述如何维护最好保存为名称/值对的应用程序信息，例如配置信息或全局设置。|  
|[如何︰ 更改整个 XML 树 (Visual Basic 中) Namespace](../../../../visual-basic/programming-guide/concepts/linq/how-to-change-the-namespace-for-an-entire-xml-tree.md)|演示如何将 XML 树从一个命名空间移动到另一个命名空间。|  
  
## <a name="see-also"></a>另请参阅  
 [编程指南 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
