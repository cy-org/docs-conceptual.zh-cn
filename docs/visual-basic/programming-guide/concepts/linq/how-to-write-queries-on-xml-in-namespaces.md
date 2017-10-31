---
title: "如何︰ 编写针对命名空间 (Visual Basic 中) 中的 XML 的查询 |Microsoft 文档"
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
ms.assetid: 7d4131b5-3288-414f-b77c-b2edc2a1f465
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
ms.openlocfilehash: 5af26b7ec0a2ab465917cd0ee62f65a97f5f0e40
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-write-queries-on-xml-in-namespaces-visual-basic"></a>如何︰ 编写针对命名空间 (Visual Basic 中) 中的 XML 的查询
若要针对的是命名空间中的 XML 编写查询，必须使用<xref:System.Xml.Linq.XName>具有正确的命名空间的对象。</xref:System.Xml.Linq.XName>  
  
 在 Visual Basic 中，最常用的方法是定义一个全局命名空间，然后使用那些使用该全局命名空间的 XML 文本和 XML 属性。 您可以定义一个全局默认命名空间，在这种情况中，XML 文本中的元素将默认位于该命名空间中。 或者，您可以定义一个具有前缀的全局命名空间，然后根据需要在 XML 文本和 XML 属性中使用该前缀。 与其他形式的 XML 一样，默认情况下，属性始终不在任何命名空间中。  
  
 本主题中示例的第一组演示如何在默认命名空间中创建 XML 树。 第二个集演示如何在具有前缀的命名空间中创建 XML 树。  
  
## <a name="example"></a>示例  
 下面的示例创建一个位于默认命名空间中的 XML 树。 然后检索元素的集合。  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child>1</Child>  
                <Child>2</Child>  
                <Child>3</Child>  
                <AnotherChild>4</AnotherChild>  
                <AnotherChild>5</AnotherChild>  
                <AnotherChild>6</AnotherChild>  
            </Root>  
        Dim c1 As IEnumerable(Of XElement) = _  
            From el In root.<Child> _  
            Select el  
        For Each el As XElement In c1  
            Console.WriteLine(el.Value)  
        Next  
    End Sub  
End Module  
```  
  
 该示例产生下面的输出：  
  
```  
1  
2  
3  
```  
  
## <a name="example"></a>示例  
 但是，在 Visual Basic 中，在使用带前缀的命名空间的 XML 树上编写查询与在默认命名空间中查询 XML 树却大不相同。 您通常使用 `Imports` 语句导入带前缀的命名空间。 然后在构造 XML 树时，在元素和属性名称中使用该前缀。 使用 XML 属性查询 XML 树时，还要使用前缀。  
  
 下面的示例创建一个位于具有前缀的默认命名空间中的 XML 树。 然后检索元素的集合。  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <aw:Child>1</aw:Child>  
                <aw:Child>2</aw:Child>  
                <aw:Child>3</aw:Child>  
                <aw:AnotherChild>4</aw:AnotherChild>  
                <aw:AnotherChild>5</aw:AnotherChild>  
                <aw:AnotherChild>6</aw:AnotherChild>  
            </aw:Root>  
        Dim c1 As IEnumerable(Of XElement) = _  
            From el In root.<aw:Child> _  
            Select el  
        For Each el As XElement In c1  
            Console.WriteLine(CInt(el))  
        Next  
    End Sub  
End Module  
```  
  
 该示例产生下面的输出：  
  
```  
1  
2  
3  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 XML 命名空间 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)
