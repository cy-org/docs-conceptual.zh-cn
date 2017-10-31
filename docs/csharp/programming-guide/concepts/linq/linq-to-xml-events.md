---
title: "LINQ to XML 事件 (C#)"
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
ms.assetid: ce7de951-cba7-4870-9962-733eb01cd680
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
ms.openlocfilehash: 5ccc3928795f188b7cf7b23d88a1f35ff043b889
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="linq-to-xml-events-c"></a>LINQ to XML 事件 (C#)
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 事件使你可以在 XML 树发生改变时得到通知。  
  
 可以将事件添加到任何 <xref:System.Xml.Linq.XObject> 的实例。 事件处理程序然后将接收对该 <xref:System.Xml.Linq.XObject> 及其所有子代进行修改的事件。 例如，可以将事件处理程序添加到树根，然后从该事件处理程序中处理对树进行的所有修改。  
  
 有关 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 事件的示例，请参阅 <xref:System.Xml.Linq.XObject.Changing> 和 <xref:System.Xml.Linq.XObject.Changed>。  
  
## <a name="types-and-events"></a>类型和事件  
 在处理事件时使用下面的类型：  
  
|类型|描述|  
|----------|-----------------|  
|<xref:System.Xml.Linq.XObjectChange>|当 <xref:System.Xml.Linq.XObject> 发生事件时指定事件类型。|  
|<xref:System.Xml.Linq.XObjectChangeEventArgs>|提供有关 <xref:System.Xml.Linq.XObject.Changing> 和 <xref:System.Xml.Linq.XObject.Changed> 事件的数据。|  
  
 修改 XML 树时将引发以下事件：  
  
|Event|描述|  
|-----------|-----------------|  
|<xref:System.Xml.Linq.XObject.Changing>|在此 <xref:System.Xml.Linq.XObject> 或它的任何子代即将发生更改之前发生。|  
|<xref:System.Xml.Linq.XObject.Changed>|在 <xref:System.Xml.Linq.XObject> 或它的任何子代已经更改时发生。|  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 当您希望在 XML 树中保留一些聚合信息时事件非常有用。 例如，您可能想保留一份发票合计，计算发票上各个项目的总和。 本示例使用事件来维护复杂元素 `Items` 之下所有子元素的总和。  
  
### <a name="code"></a>代码  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Total", "0"),  
    new XElement("Items")  
);  
XElement total = root.Element("Total");  
XElement items = root.Element("Items");  
items.Changed += (object sender, XObjectChangeEventArgs cea) =>  
{  
    switch (cea.ObjectChange)  
    {  
        case XObjectChange.Add:  
            if (sender is XElement)  
                total.Value = ((int)total + (int)(XElement)sender).ToString();  
            if (sender is XText)  
                total.Value = ((int)total + (int)((XText)sender).Parent).ToString();  
            break;  
        case XObjectChange.Remove:  
            if (sender is XElement)  
                total.Value = ((int)total - (int)(XElement)sender).ToString();  
            if (sender is XText)  
                total.Value = ((int)total - Int32.Parse(((XText)sender).Value)).ToString();  
            break;  
    }  
    Console.WriteLine("Changed {0} {1}",  
      sender.GetType().ToString(), cea.ObjectChange.ToString());  
};  
items.SetElementValue("Item1", 25);  
items.SetElementValue("Item2", 50);  
items.SetElementValue("Item2", 75);  
items.SetElementValue("Item3", 133);  
items.SetElementValue("Item1", null);  
items.SetElementValue("Item4", 100);  
Console.WriteLine("Total:{0}", (int)total);  
Console.WriteLine(root);  
```  
  
### <a name="comments"></a>注释  
 此代码生成以下输出：  
  
```  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XText Remove  
Changed System.Xml.Linq.XText Add  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XElement Remove  
Changed System.Xml.Linq.XElement Add  
Total:308  
<Root>  
  <Total>308</Total>  
  <Items>  
    <Item2>75</Item2>  
    <Item3>133</Item3>  
    <Item4>100</Item4>  
  </Items>  
</Root>  
```  
  
## <a name="see-also"></a>请参阅  
 [高级 LINQ to XML 编程 (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)

