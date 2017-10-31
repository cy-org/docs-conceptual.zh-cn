---
title: "如何︰ 投影新类型 (LINQ to XML) (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 8cfb24f5-89b2-4cfb-b85d-e7963f8f1845
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a7cbbce130aa78a7e14ffd61a1dcd76b969e1b35
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-project-a-new-type-linq-to-xml-visual-basic"></a>如何︰ 投影新类型 (LINQ to XML) (Visual Basic)
本部分中的其他示例已演示查询返回的结果作为<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>，<xref:System.Collections.Generic.IEnumerable%601>的`string`，和<xref:System.Collections.Generic.IEnumerable%601>的`int`。</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 这些是常见结果类型，但它们不是对所有情况都适用。 在许多情况下，您会希望查询返回<xref:System.Collections.Generic.IEnumerable%601>的某些其他类型。</xref:System.Collections.Generic.IEnumerable%601>  
  
## <a name="example"></a>示例  
 此示例演示如何在 `Select` 子句中实例化对象。 代码首先定义一个具有一个构造函数的新类，然后修改 `Select` 语句，使该表达式成为新类的新实例。  
  
 此示例使用下面的 XML 文档︰[示例 XML 文件︰ 典型采购订单 (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml.md)。  
  
```vb  
Public Class NameQty  
    Public name As String  
    Public qty As Integer  
    Public Sub New(ByVal n As String, ByVal q As Integer)  
        name = n  
        qty = q  
    End Sub  
End Class  
  
Public Class Program  
    Shared Sub Main()  
        Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
  
        Dim nqList As IEnumerable(Of NameQty) = _  
            From n In po...<Item> _  
            Select New NameQty( _  
                n.<ProductName>.Value, CInt(n.<Quantity>.Value))  
  
        For Each n As NameQty In nqList  
            Console.WriteLine(n.name & ":" & n.qty)  
        Next  
    End Sub  
End Class  
```  
  
 此示例使用`M:System.Xml.Linq.XElement.Element`主题中引入的方法[如何︰ 检索单个子元素 (LINQ to XML) (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-child-element-linq-to-xml.md)。 还使用强制转换来检索 `M:System.Xml.Linq.XElement.Element` 方法返回的元素值。  
  
 该示例产生下面的输出：  
  
```  
Lawnmower:1  
Baby Monitor:2  
```  
  
## <a name="see-also"></a>另请参阅  
 [投影和转换 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
