---
title: "维护名称-值对 (C#)"
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
ms.assetid: 7b04b0f1-af64-42eb-8737-83f8861b5915
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9515411123ad800df4e800d698921b76f6590286
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="maintaining-namevalue-pairs-c"></a>维护名称/值对 (C#)
很多应用程序都必须维护需要保存为名称/值对的信息。 此信息可能是配置信息或全局设置。 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 包含一些方法，能轻松保存一组名称/值对。 可以将这些信息保存为属性，也可以保存为一组子元素。  
  
 将信息保存为属性和保存为子元素之间的区别在于属性具有约束，对于一个元素，只能有一个属性具有特定的名称。 而这种限制不适用于子元素。  
  
## <a name="setattributevalue-and-setelementvalue"></a>SetAttributeValue 与 SetElementValue  
 两种有助于保存名称/值对的方法是 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> 和 <xref:System.Xml.Linq.XElement.SetElementValue%2A>。 这两种方法具有相似的语义。  
  
 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> 可以添加、修改或移除元素的属性。  
  
-   如果使用不存在的属性的名称调用 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>，则该方法会创建一个新属性并将该属性添加到指定的元素中。  
  
-   如果使用现有属性的名称调用 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>，并指定一些内容，则会用指定内容替换属性的内容。  
  
-   如果使用现有属性的名称调用 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>，并指定内容为空，则会从该属性的父级移除该属性。  
  
 <xref:System.Xml.Linq.XElement.SetElementValue%2A> 可以添加、修改或移除元素的子元素。  
  
-   如果使用不存在的子元素的名称调用 <xref:System.Xml.Linq.XElement.SetElementValue%2A>，则该方法会创建一个新元素并将该新元素添加到指定的元素中。  
  
-   如果使用现有元素的名称调用 <xref:System.Xml.Linq.XElement.SetElementValue%2A>，并指定一些内容，则会用指定内容替换元素的内容。  
  
-   如果使用现有元素的名称调用 <xref:System.Xml.Linq.XElement.SetElementValue%2A>，并指定内容为空，则会从该元素的父级移除该元素。  
  
## <a name="example"></a>示例  
 下面的示例创建一个没有属性的元素。 之后使用 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> 方法创建一个名称/值对列表并维护该列表。  
  
```csharp  
// Create an element with no content.  
XElement root = new XElement("Root");  
  
// Add a number of name/value pairs as attributes.  
root.SetAttributeValue("Top", 22);  
root.SetAttributeValue("Left", 20);  
root.SetAttributeValue("Bottom", 122);  
root.SetAttributeValue("Right", 300);  
root.SetAttributeValue("DefaultColor", "Color.Red");  
Console.WriteLine(root);  
  
// Replace the value of Top.  
root.SetAttributeValue("Top", 10);  
Console.WriteLine(root);  
  
// Remove DefaultColor.  
root.SetAttributeValue("DefaultColor", null);  
Console.WriteLine(root);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Root Top="22" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" />  
```  
  
## <a name="example"></a>示例  
 下面的示例创建一个没有子元素的元素。 之后使用 <xref:System.Xml.Linq.XElement.SetElementValue%2A> 方法创建一个名称/值对列表并维护该列表。  
  
```csharp  
// Create an element with no content.  
XElement root = new XElement("Root");  
  
// Add a number of name/value pairs as elements.  
root.SetElementValue("Top", 22);  
root.SetElementValue("Left", 20);  
root.SetElementValue("Bottom", 122);  
root.SetElementValue("Right", 300);  
root.SetElementValue("DefaultColor", "Color.Red");  
Console.WriteLine(root);  
Console.WriteLine("----");  
  
// Replace the value of Top.  
root.SetElementValue("Top", 10);  
Console.WriteLine(root);  
Console.WriteLine("----");  
  
// Remove DefaultColor.  
root.SetElementValue("DefaultColor", null);  
Console.WriteLine(root);  
```  
  
 该示例产生下面的输出：  
  
```xml  
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
 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>   
 <xref:System.Xml.Linq.XElement.SetElementValue%2A>   
 [修改 XML 树 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)

