---
title: "如何：通过对标头信息的访问流式处理 XML 片段 (C#)"
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
ms.assetid: 7f242770-b0c7-418d-894b-643215e1f8aa
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
ms.openlocfilehash: b7a83c9fc88b6e59cc1c8308d92464591896d312
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-stream-xml-fragments-with-access-to-header-information-c"></a>如何：通过对标头信息的访问流式处理 XML 片段 (C#)
有时，您必须读取任意大的 XML 文件并在编写您的应用程序时可以预测应用程序的内存需求量。 如果您试图用大 XML 文件填充 XML 树，则内存占用量将与文件大小成正比，也就是说会占用过多内存。 因此，您应改用流处理技术。  
  
 一种选择是使用 <xref:System.Xml.XmlReader> 来编写应用程序。 但您可能需要使用 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 来查询 XML 树。 在这种情况下，您可以编写自己的自定义轴方法。 有关详细信息，请参阅[如何：编写 LINQ to XML 轴方法 (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-write-a-linq-to-xml-axis-method.md)。  
  
 若要编写您自己的轴方法，请编写一个小方法，让该方法使用 <xref:System.Xml.XmlReader> 来读取各个节点，直到达到您感兴趣的节点之一。 该方法然后调用 <xref:System.Xml.Linq.XNode.ReadFrom%2A>，后者将从 <xref:System.Xml.XmlReader> 中读取数据并实例化 XML 片段。 然后，该方法生成从 `yield return` 到该方法（枚举您的自定义轴方法的方法）的每个片段。 然后，您可以对自定义轴方法编写 LINQ 查询。  
  
 流处理技术最适合只需处理一次源文档的情况，您可以按文档顺序处理各个元素。 某些标准查询运算符（如 <xref:System.Linq.Enumerable.OrderBy%2A>）可以循环访问其源、收集所有数据、对数据排序，最后生成序列中的第一项。 请注意，如果使用可在生成第一项之前具体化源的查询运算符，则不会保持小的内存需求量。  
  
## <a name="example"></a>示例  
 有时，问题会变得更有意思。 在下面的 XML 文档中，自定义轴方法的使用方也必须知道每一项所属的使用方名称。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<Root>  
  <Customer>  
    <Name>A. Datum Corporation</Name>  
    <Item>  
      <Key>0001</Key>  
    </Item>  
    <Item>  
      <Key>0002</Key>  
    </Item>  
    <Item>  
      <Key>0003</Key>  
    </Item>  
    <Item>  
      <Key>0004</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Fabrikam, Inc.</Name>  
    <Item>  
      <Key>0005</Key>  
    </Item>  
    <Item>  
      <Key>0006</Key>  
    </Item>  
    <Item>  
      <Key>0007</Key>  
    </Item>  
    <Item>  
      <Key>0008</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Southridge Video</Name>  
    <Item>  
      <Key>0009</Key>  
    </Item>  
    <Item>  
      <Key>0010</Key>  
    </Item>  
  </Customer>  
</Root>  
```  
  
 本示例采用的方法还将监视此标头信息、保存标头信息，然后生成包含标头信息和所要枚举的详细信息的小型 XML 树。 该轴方法然后生成这个新的小型 XML 树。 之后，查询将可以访问标头信息以及详细信息。  
  
 此方法具有小的内存需求量。 由于生成了所有的详细 XML 片段，不再需要保留对前一个片段的引用，因此，此方法可用于垃圾回收。 请注意，此技术会在堆上创建许多短生存期的对象。  
  
 下面的示例演示如何实现和使用可流处理由 URI 指定的文件中的 XML 片段的自定义轴方法。 此自定义轴经过专门编写，可以处理具有 `Customer`、`Name` 和 `Item` 元素，并且这些元素按上述 `Source.xml` 文档排列的文档。 这是一个过于简单的实现。 将会准备一个更可靠的实现以分析无效文档。  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null) {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    XElement xmlTree = new XElement("Root",  
        from el in StreamCustomerItem("Source.xml")  
        where (int)el.Element("Key") >= 3 && (int)el.Element("Key") <= 7  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        )  
    );  
    Console.WriteLine(xmlTree);  
}  
```  
  
 此代码生成以下输出：  
  
```xml  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
</Root>  
```  
  
## <a name="see-also"></a>请参阅  
 [高级 LINQ to XML 编程 (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)

