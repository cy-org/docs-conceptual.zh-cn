---
title: "内存中 XML 树修改与功能构造 (LINQ to XML) (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: d91c4ebf-6549-43cc-9961-26d4a82f722b
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0456d221f01573e6ef1c67a3e0d1db585e6f3b0c
ms.lasthandoff: 03/13/2017


---
# <a name="in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml-visual-basic"></a>内存中 XML 树修改与功能构造 (LINQ to XML) (Visual Basic)
就地修改 XML 树是更改 XML 文档形状的传统方法。 典型的应用程序将文档加载到数据存储区（如 DOM 或 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]）；使用编程接口插入节点、删除节点或更改节点的内容；然后将 XML 保存到文件或通过网络传输。  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]允许在许多方案中非常有用的另一种方法*︰ 函数构造*。 函数构造将修改数据视为转换问题，而不是数据存储区的具体操作。 如果您采用某种数据表示形式并有效地将其从一种形式转换为另一种形式，其结果等效于您采用一个数据存储区并对其以某种方式进行操作以采用另一种形状。 函数构造方法的关键是要传递到查询的结果<xref:System.Xml.Linq.XDocument>和<xref:System.Xml.Linq.XElement>构造函数。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument>  
  
 在许多情况下，您可以在操作数据存储区所需的很短时间内编写转换代码，并且该代码更稳定、更易于维护。 在这些情况下，虽然转换方法可能具有较强的处理能力，但它更适合用于修改数据。 如果开发人员熟悉函数方法，则在很多情况下，生成的代码会更易于理解。 可以很容易地找到修改树的每部分的代码。  
  
 DOM 程序员更熟悉就地修改 XML 树的方法，而不了解这种方法的开发人员可能会对使用函数方法编写的代码感到陌生。 如果您必须对大型 XML 树进行小修改，则在很多情况下，用于就地修改树的方法将花费更少的 CPU 时间。  
  
 本主题提供用这两种方法实现的一个示例。  
  
## <a name="transforming-attributes-into-elements"></a>将属性转换为元素  
 此示例假设您想修改下面的简单 XML 文档，使属性变为元素。 本节首先介绍传统的就地修改方法。 然后显示函数构造方法。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<Root Data1="123" Data2="456">  
  <Child1>Content</Child1>  
</Root>  
```  
  
### <a name="modifying-the-xml-tree"></a>修改 XML 树  
 您可以编写一些过程代码以便从属性创建元素，然后删除属性，如下所示：  
  
```vb  
Dim root As XElement = XElement.Load("Data.xml")  
For Each att As XAttribute In root.Attributes()  
    root.Add(New XElement(att.Name, att.Value))  
Next  
root.Attributes().Remove()  
Console.WriteLine(root)  
```  
  
 此代码生成以下输出：  
  
```xml  
<Root>  
  <Child1>Content</Child1>  
  <Data1>123</Data1>  
  <Data2>456</Data2>  
</Root>  
```  
  
### <a name="functional-construction-approach"></a>函数构造方法  
 相比之下，函数方法包含用于形成新树的代码、从源树中选择元素和属性并在将其添加到新树中时进行相应的转换。 函数方法如下所示：  
  
```vb  
Dim root As XElement = XElement.Load("Data.xml")  
Dim newTree As XElement = _  
    <Root>  
        <%= root.<Child1> %>  
        <%= From att In root.Attributes() _  
            Select New XElement(att.Name, att.Value) %>  
    </Root>  
Console.WriteLine(newTree)  
```  
  
 本示例与第一个示例输出相同的 XML。 但请注意，您可以在函数方法中实际看到生成的新 XML 的结构。 您可以看到创建 `Root` 元素的代码、从源树中提取 `Child1` 元素的代码和将源树中的属性转换为新树中的元素的代码。  
  
 在本例中，函数示例一点也不比第一个示例简短，而且一点也不比第一个示例简单。 但如果要对一个 XML 树进行很多更改，则非函数方法将变得非常复杂，而且会显得很笨拙。 相比之下，使用函数方法时，您只需形成所需的 XML，嵌入适当的查询和表达式以提取需要的内容。 函数方法生成的代码更易于维护。  
  
 请注意，在本例中，函数方法的执行效果可能没有树操作方法好。 主要问题是函数方法创建了更多短生存期的对象。 但是，如果使用函数方法能够提高程序员的效率，则折中也是一种有效的方式。  
  
 这是一个很简单的示例，但它显示了这两种方法之间基本原理上的差异。 对于转换较大的 XML 文档，函数方法可以产生更高的效率增益。  
  
## <a name="see-also"></a>另请参阅  
 [修改 XML 树 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
