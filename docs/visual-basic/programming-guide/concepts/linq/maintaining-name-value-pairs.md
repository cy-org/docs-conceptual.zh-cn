---
title: "维护名称 / 值对 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 57ac2072-d9f5-432b-84f0-a889c62fd813
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 54db297ecd39e37492dcf8bb4de4f64476662670
ms.lasthandoff: 03/13/2017


---
# <a name="maintaining-namevalue-pairs-visual-basic"></a>维护名称/值对 (Visual Basic)
很多应用程序都必须维护需要保存为名称/值对的信息。 此信息可能是配置信息或全局设置。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 包含一些方法，能轻松保存一组名称/值对。 可以将这些信息保存为属性，也可以保存为一组子元素。  
  
 将信息保存为属性和保存为子元素之间的区别在于属性具有约束，对于一个元素，只能有一个属性具有特定的名称。 而这种限制不适用于子元素。  
  
## <a name="setattributevalue-and-setelementvalue"></a>SetAttributeValue 与 SetElementValue  
 两种方法中有助于保存名称/值对是<xref:System.Xml.Linq.XElement.SetAttributeValue%2A>和<xref:System.Xml.Linq.XElement.SetElementValue%2A>。</xref:System.Xml.Linq.XElement.SetElementValue%2A> </xref:System.Xml.Linq.XElement.SetAttributeValue%2A> 这两种方法具有相似的语义。  
  
 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>可以添加、 修改或删除元素的属性。</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
-   如果调用<xref:System.Xml.Linq.XElement.SetAttributeValue%2A>具有不存在的属性名称，该方法创建新的属性并将其添加到指定的元素。</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
-   如果调用<xref:System.Xml.Linq.XElement.SetAttributeValue%2A>现有属性的名称，并指定一些内容，该属性的内容会用替换为指定的内容。</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
-   如果调用<xref:System.Xml.Linq.XElement.SetAttributeValue%2A>对现有的同名属性，并指定内容为空，则移除该属性从其父级。</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
 <xref:System.Xml.Linq.XElement.SetElementValue%2A>可以添加、 修改或删除元素的子元素。</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
-   如果调用<xref:System.Xml.Linq.XElement.SetElementValue%2A>与不存在的子元素的名称，该方法创建一个新元素，并将其添加到指定的元素。</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
-   如果调用<xref:System.Xml.Linq.XElement.SetElementValue%2A>现有元素的名称，并指定一些内容，该元素的内容会用替换为指定的内容。</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
-   如果调用<xref:System.Xml.Linq.XElement.SetElementValue%2A>了一个名为现有的元素，并指定内容为空，从其父级中移除该元素。</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
## <a name="example"></a>示例  
 下面的示例创建一个没有属性的元素。 然后，它使用<xref:System.Xml.Linq.XElement.SetAttributeValue%2A>方法来创建和维护名称/值对的列表。</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
```vb  
' Create an element with no content.  
Dim root As XElement = <Root/>  
  
' Add a number of name/value pairs as attributes.  
root.SetAttributeValue("Top", 22)  
root.SetAttributeValue("Left", 20)  
root.SetAttributeValue("Bottom", 122)  
root.SetAttributeValue("Right", 300)  
root.SetAttributeValue("DefaultColor", "Color.Red")  
Console.WriteLine(root)  
  
' Replace the value of Top.  
root.SetAttributeValue("Top", 10)  
Console.WriteLine(root)  
  
' Remove DefaultColor.  
root.SetAttributeValue("DefaultColor", Nothing)  
Console.WriteLine(root)  
```  
  
 该示例产生下面的输出：  
  
```  
<Root Top="22" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" />  
```  
  
## <a name="example"></a>示例  
 下面的示例创建一个没有子元素的元素。 然后，它使用<xref:System.Xml.Linq.XElement.SetElementValue%2A>方法来创建和维护名称/值对的列表。</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
```vb  
' Create an element with no content.  
Dim root As XElement = <Root/>  
  
' Add a number of name/value pairs as elements.  
root.SetElementValue("Top", 22)  
root.SetElementValue("Left", 20)  
root.SetElementValue("Bottom", 122)  
root.SetElementValue("Right", 300)  
root.SetElementValue("DefaultColor", "Color.Red")  
Console.WriteLine(root)  
Console.WriteLine("----")  
  
' Replace the value of Top.  
root.SetElementValue("Top", 10)  
Console.WriteLine(root)  
Console.WriteLine("----")  
  
' Remove DefaultColor.  
root.SetElementValue("DefaultColor", Nothing)  
Console.WriteLine(root)  
  
```  
  
 该示例产生下面的输出：  
  
```  
<Root>  
  <Top>22</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
  <DefaultColor>Color.Red</DefaultColor>  
</Root>  
----  
<Root>  
  <Top>10</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
  <DefaultColor>Color.Red</DefaultColor>  
</Root>  
----  
<Root>  
  <Top>10</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
</Root>  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A></xref:System.Xml.Linq.XElement.SetAttributeValue%2A>   
 <xref:System.Xml.Linq.XElement.SetElementValue%2A></xref:System.Xml.Linq.XElement.SetElementValue%2A>   
 [修改 XML 树 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
