---
title: "功能构造 (LINQ to XML) (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: feac4273-39ab-43ae-bab7-4059c807a785
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
ms.openlocfilehash: 9fa8cb3c97a1e23a863296c828c82b240e9ab5db
ms.lasthandoff: 03/13/2017

---
# <a name="functional-construction-linq-to-xml-visual-basic"></a>功能构造 (LINQ to XML) (Visual Basic)
[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]提供了一种功能强大的方法来创建 XML 元素名*功能性构造法*。 函数构造是指在单个语句中创建 XML 树的能力。  
  
 启用函数构造的 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 编程接口有几个重要功能：  
  
-   <xref:System.Xml.Linq.XElement>构造函数采用多种类型的参数的内容。</xref:System.Xml.Linq.XElement> 例如，可以传递另一个<xref:System.Xml.Linq.XElement>对象，它将成为子元素。</xref:System.Xml.Linq.XElement> 您可以将传递<xref:System.Xml.Linq.XAttribute>对象，它将成为该元素的一个属性。</xref:System.Xml.Linq.XAttribute> 也可以传递任何其他类型的对象，该对象将转换为字符串并成为该元素的文本内容。  
  
-   <xref:System.Xml.Linq.XElement>构造函数采用`params`类型的数组<xref:System.Object>，以便可以将任意数量的对象传递给构造函数。</xref:System.Object> </xref:System.Xml.Linq.XElement> 这使您可以创建具有复杂内容的元素。  
  
-   如果对象实现<xref:System.Collections.Generic.IEnumerable%601>，枚举中对象的集合，并添加集合中的所有项。</xref:System.Collections.Generic.IEnumerable%601> 如果集合包含<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XAttribute>对象，则单独添加集合中的每个项。</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> 这一功能很重要，因为它允许您将 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询的结果传递给构造函数。  
  
 下面是一个示例：  
  
 这些功能使您能够编写代码以创建 XML 树，以及编写使用的结果的代码使用 XML 文本[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询创建 XML 树时︰  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element>1</Element>  
        <Element>2</Element>  
        <Element>3</Element>  
        <Element>4</Element>  
        <Element>5</Element>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child>1</Child>  
        <Child>2</Child>  
        <%= From el In srcTree.Elements() _  
            Where CInt(el) > 2 _  
            Select el %>  
    </Root>  
Console.WriteLine(xmlTree)  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建 XML 树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
