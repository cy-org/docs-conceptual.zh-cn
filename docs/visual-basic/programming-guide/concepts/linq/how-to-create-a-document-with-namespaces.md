---
title: "如何︰ 创建包含命名空间 (LINQ to XML) 的文档 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: cc5b0d4d-360c-4ada-94fa-2d2916e989be
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
ms.openlocfilehash: 761967351cfc6292eb60a5941e213bfd90036f65
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-document-with-namespaces-linq-to-xml-visual-basic"></a>如何：使用命名空间创建文档 (LINQ to XML) (Visual Basic)
本主题演示如何在 Visual Basic 中创建包含命名空间的文档。  
  
 在 Visual Basic 中使用 XML 文本时，用户可以定义一个全局默认 XML 命名空间。 该命名空间对 XML 文本和 XML 属性都是默认的命名空间。 可以在项目级别或文件级别上定义默认的 XML 命名空间。 如果在文件级别上定义，则会重写项目级别上的默认命名空间。  
  
 还可以定义其他命名空间，并为这些命名空间指定命名空间前缀。  
  
 通过使用 `Imports` 关键字来定义默认命名空间和带前缀的命名空间。  
  
 有关详细信息，请参阅[在 Visual Basic 中的 XML 文本简介](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-xml-literals.md)。  
  
 请注意，默认 XML 命名空间仅适用于元素，而不适用于属性。 默认情况下属性从不在命名空间中。 但是可以使用命名空间前缀将属性置于一个命名空间中。  
  
## <a name="example"></a>示例  
 此示例创建一个包含命名空间的文档。  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <aw:Child aw:Att="attvalue"/>  
            </aw:Root>  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 该示例产生下面的输出：  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Child aw:Att="attvalue" />  
</aw:Root>  
```  
  
## <a name="example"></a>示例  
 此示例创建一个包含两个命名空间的文档，其中一个为默认命名空间。  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
Imports <xmlns:fc="www.fourthcoffee.com">  
  
Module Module1  
  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child Att="attvalue"/>  
                <fc:Child2>child2 content</fc:Child2>  
            </Root>  
        Console.WriteLine(root)  
    End Sub  
  
End Module  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Root xmlns:fc="www.fourthcoffee.com" xmlns="http://www.adventure-works.com">  
  <Child Att="attvalue" />  
  <fc:Child2>child2 content</fc:Child2>  
</Root>  
```  
  
## <a name="example"></a>示例  
 下面的示例创建一个包含多个命名空间的文档，每个命名空间都具有命名空间前缀。  
  
 序列化 XML 树时，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 发出所需的命名空间声明，这样每个元素都位于所指定的命名空间中。  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
Imports <xmlns:fc="www.fourthcoffee.com">  
  
Module Module1  
  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <fc:Child>  
                    <aw:DifferentChild>other content</aw:DifferentChild>  
                </fc:Child>  
                <aw:Child2>c2 content</aw:Child2>  
                <fc:Child3>c3 content</fc:Child3>  
            </aw:Root>  
        Console.WriteLine(root)  
    End Sub  
  
End Module  
```  
  
 该示例产生下面的输出：  
  
```xml  
<aw:Root xmlns:fc="www.fourthcoffee.com" xmlns:aw="http://www.adventure-works.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 XML 命名空间 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)
