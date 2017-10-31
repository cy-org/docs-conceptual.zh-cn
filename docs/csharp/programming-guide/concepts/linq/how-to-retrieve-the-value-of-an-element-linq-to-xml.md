---
title: "如何：检索元素的值 (LINQ to XML) (C#)"
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
ms.assetid: 4228c007-07c9-4cf2-a45b-e7074c109581
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 70e60c799157c7aa577bb8abd1fa6aaad746d3d1
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-retrieve-the-value-of-an-element-linq-to-xml-c"></a>如何：检索元素的值 (LINQ to XML) (C#)
本主题演示如何获取元素的值。 有两种主要方法可以完成此操作。 一种方法是将 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XAttribute> 强制转换为所需的类型。 然后，显式转换运算符将元素或属性的内容转换为指定的类型，并将其分配给变量。 此外，还可以使用 <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=fullName> 属性或 <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName> 属性。  
  
 但是，对于 C#，强制转换通常是更好的方法。 在检索可能存在也可能不存在的元素（或属性）的值时，如果将元素或属性强制转换为可以为 null 的类型，则代码会更易于编写。 本主题最后一个示例对此进行了演示。 但是，无法通过强制转换设置元素的内容，而通过 <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=fullName> 属性可以做到这一点。  
  
## <a name="example"></a>示例  
 若要检索元素的值，只需将 <xref:System.Xml.Linq.XElement> 对象强制转换为所需的类型即可。 任何时候都可以将元素强制转换为字符串，如下所示：  
  
```csharp  
XElement e = new XElement("StringElement", "abcde");  
Console.WriteLine(e);  
Console.WriteLine("Value of e:" + (string)e);  
```  
  
 该示例产生下面的输出：  
  
```  
<StringElement>abcde</StringElement>  
Value of e:abcde  
```  
  
## <a name="example"></a>示例  
 此外，还可以将元素强制转换为字符串以外的其他类型。 例如，如果有一个包含一个整数的元素，可以将它强制转换为 `int`，如下面的代码所示：  
  
```csharp  
XElement e = new XElement("Age", "44");  
Console.WriteLine(e);  
Console.WriteLine("Value of e:" + (int)e);  
```  
  
 该示例产生下面的输出：  
  
```  
<Age>44</Age>  
Value of e:44  
```  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 提供了以下数据类型的显式强制转换运算符：`string`、`bool`、`bool?`、`int`、`int?`、`uint`、`uint?`、`long`、`long?`、`ulong`、`ulong?`、`float`、`float?`、`double`、`double?`、`decimal`、`decimal?`、`DateTime`、`DateTime?`、`TimeSpan`、`TimeSpan?`、`GUID` 和 `GUID?`。  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 为 <xref:System.Xml.Linq.XAttribute> 对象提供了相同的强制转换运算符。  
  
## <a name="example"></a>示例  
 可以使用 <xref:System.Xml.Linq.XElement.Value%2A> 属性来检索元素的内容：  
  
```csharp  
XElement e = new XElement("StringElement", "abcde");   
Console.WriteLine(e);  
Console.WriteLine("Value of e:" + e.Value);  
```  
  
 该示例产生下面的输出：  
  
```  
<StringElement>abcde</StringElement>  
Value of e:abcde  
```  
  
## <a name="example"></a>示例  
 有时，尽管不能确定某个元素是否存在，还是会尝试检索该元素的值。 在这种情况下，将强制转换后的元素分配给可以为 null 的类型（`string` 或 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 中可以为 null 的类型之一）时，如果该元素不存在，则将分配的变量设置为 `null`。 下面的代码演示当元素可能存在也可能不存在时，使用强制转换比使用 <xref:System.Xml.Linq.XElement.Value%2A> 属性更加简单。  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Child1", "child 1 content"),  
    new XElement("Child2", "2")  
);  
  
// The following assignments show why it is easier to use  
// casting when the element might or might not exist.  
  
string c1 = (string)root.Element("Child1");  
Console.WriteLine("c1:{0}", c1 == null ? "element does not exist" : c1);  
  
int? c2 = (int?)root.Element("Child2");  
Console.WriteLine("c2:{0}", c2 == null ? "element does not exist" : c2.ToString());  
  
string c3 = (string)root.Element("Child3");  
Console.WriteLine("c3:{0}", c3 == null ? "element does not exist" : c3);  
  
int? c4 = (int?)root.Element("Child4");  
Console.WriteLine("c4:{0}", c4 == null ? "element does not exist" : c4.ToString());  
  
Console.WriteLine();  
  
// The following assignments show the required code when using  
// the Value property when the element might or might not exist.  
// Notice that this is more difficult than the casting approach.  
  
XElement e1 = root.Element("Child1");  
string v1;  
if (e1 == null)  
    v1 = null;  
else  
    v1 = e1.Value;  
Console.WriteLine("v1:{0}", v1 == null ? "element does not exist" : v1);  
  
XElement e2 = root.Element("Child2");  
int? v2;  
if (e2 == null)  
    v2 = null;  
else  
    v2 = Int32.Parse(e2.Value);  
Console.WriteLine("v2:{0}", v2 == null ? "element does not exist" : v2.ToString());  
  
XElement e3 = root.Element("Child3");  
string v3;  
if (e3 == null)  
    v3 = null;  
else  
    v3 = e3.Value;  
Console.WriteLine("v3:{0}", v3 == null ? "element does not exist" : v3);  
  
XElement e4 = root.Element("Child4");  
int? v4;  
if (e4 == null)  
    v4 = null;  
else  
    v4 = Int32.Parse(e4.Value);  
Console.WriteLine("v4:{0}", v4 == null ? "element does not exist" : v4.ToString());  
```  
  
 此代码生成以下输出：  
  
```  
c1:child 1 content  
c2:2  
c3:element does not exist  
c4:element does not exist  
  
v1:child 1 content  
v2:2  
v3:element does not exist  
v4:element does not exist  
```  
  
 通常情况下，当使用强制转换来检索元素和属性的内容时，可以编写更简易的代码。  
  
## <a name="see-also"></a>请参阅  
 [LINQ to XML 轴 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)

