---
title: "XDocument 类概述 (C#)"
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
ms.assetid: 63305603-ab54-49fc-84e4-f76eecc59549
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
ms.openlocfilehash: 2e8513c8c969f7522866454838c6c08da528c1b6
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="xdocument-class-overview-c"></a>XDocument 类概述 (C#)
本主题介绍 <xref:System.Xml.Linq.XDocument> 类。  
  
## <a name="overview-of-the-xdocument-class"></a>XDocument 类概述  
 <xref:System.Xml.Linq.XDocument> 类包含有效的 XML 文档所需的信息。 其中包括 XML 声明、处理指令和注释。  
  
 请注意，如果需要 <xref:System.Xml.Linq.XDocument> 类提供的特定功能，您只需创建 <xref:System.Xml.Linq.XDocument> 对象。 在很多情况下，可以直接使用 <xref:System.Xml.Linq.XElement>。 直接使用 <xref:System.Xml.Linq.XElement> 是一种比较简单的编程模型。  
  
 <xref:System.Xml.Linq.XDocument> 派生自 <xref:System.Xml.Linq.XContainer>。 因此，它可以包含子节点。 但是，<xref:System.Xml.Linq.XDocument> 对象只能有一个子 <xref:System.Xml.Linq.XElement> 节点。 这反映了 XML 标准，即在 XML 文档中只能有一个根元素。  
  
## <a name="components-of-xdocument"></a>Xdocument 的组件  
 <xref:System.Xml.Linq.XDocument> 可以包含以下元素：  
  
-   一个 <xref:System.Xml.Linq.XDeclaration> 对象。 <xref:System.Xml.Linq.XDeclaration> 使您能够指定 XML 声明的相关部分：XML 版本、文档的编码以及 XML 文档是否是独立的。  
  
-   一个 <xref:System.Xml.Linq.XElement> 对象。 这是 XML 文档的根节点。  
  
-   任意数目的 <xref:System.Xml.Linq.XProcessingInstruction> 对象。 处理指令将信息传递给处理 XML 的应用程序。  
  
-   任意数目的 <xref:System.Xml.Linq.XComment> 对象。 注释将与根元素同级。 <xref:System.Xml.Linq.XComment> 对象不能是列表中的第一个参数，因为 XML 文档以注释开头无效。  
  
-   一个用于 DTD 的 <xref:System.Xml.Linq.XDocumentType>。  
  
 序列化 <xref:System.Xml.Linq.XDocument> 时，即使 `XDocument.Declaration` 为 `null`，输出也将具有 XML 声明，前提是编写器已经将 `Writer.Settings.OmitXmlDeclaration` 设置为 `false`（默认值）。  
  
 默认情况下，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 将版本设置为“1.0”，将编码设置为“utf-8”。  
  
## <a name="using-xelement-without-xdocument"></a>在没有 Xdocument 的情况下使用 XElement  
 如上所述，<xref:System.Xml.Linq.XElement> 类是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 编程接口中的主类。 在很多情况下，您的应用程序不需要您创建文档。 通过使用 <xref:System.Xml.Linq.XElement> 类，可以创建 XML 树，向它添加其他 XML 树，修改 XML 树并进行保存。  
  
## <a name="using-xdocument"></a>使用 XDocument  
 若要构造一个 <xref:System.Xml.Linq.XDocument>，可使用函数构造，正如您构造 <xref:System.Xml.Linq.XElement> 对象那样。  
  
 下面的代码创建一个 <xref:System.Xml.Linq.XDocument> 对象及其关联的包含对象。  
  
```csharp  
XDocument d = new XDocument(  
    new XComment("This is a comment."),  
    new XProcessingInstruction("xml-stylesheet",  
        "href='mystyle.css' title='Compact' type='text/css'"),  
    new XElement("Pubs",  
        new XElement("Book",  
            new XElement("Title", "Artifacts of Roman Civilization"),  
            new XElement("Author", "Moreno, Jordao")  
        ),  
        new XElement("Book",  
            new XElement("Title", "Midieval Tools and Implements"),  
            new XElement("Author", "Gazit, Inbar")  
        )  
    ),  
    new XComment("This is another comment.")  
);  
d.Declaration = new XDeclaration("1.0", "utf-8", "true");  
Console.WriteLine(d);  
  
d.Save("test.xml");  
```  
  
 当你检查文件 test.xml 时, 会得到以下输出：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<!--This is a comment.-->  
<?xml-stylesheet href='mystyle.css' title='Compact' type='text/css'?>  
<Pubs>  
  <Book>  
    <Title>Artifacts of Roman Civilization</Title>  
    <Author>Moreno, Jordao</Author>  
  </Book>  
  <Book>  
    <Title>Midieval Tools and Implements</Title>  
    <Author>Gazit, Inbar</Author>  
  </Book>  
</Pubs>  
<!--This is another comment.-->  
```  
  
## <a name="see-also"></a>请参阅  
 [LINQ to XML 编程概述 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)

