---
title: "XDocument 类概述 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 45cb7e71-196a-47da-bfe9-7a5589db1eed
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
ms.openlocfilehash: 31111b23adb019aad3ad55787c073dc02446291d
ms.lasthandoff: 03/13/2017

---
# <a name="xdocument-class-overview-visual-basic"></a>XDocument 类概述 (Visual Basic)
本主题介绍了<xref:System.Xml.Linq.XDocument>类。</xref:System.Xml.Linq.XDocument>  
  
## <a name="overview-of-the-xdocument-class"></a>XDocument 类概述  
 <xref:System.Xml.Linq.XDocument>类包含有效的 XML 文档所需的信息。</xref:System.Xml.Linq.XDocument> 其中包括 XML 声明、处理指令和注释。  
  
 请注意，您只需创建<xref:System.Xml.Linq.XDocument>对象，如果您需要的特定功能，提供的<xref:System.Xml.Linq.XDocument>类。</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XDocument> 在许多情况下，您可以直接使用<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement> 直接使用<xref:System.Xml.Linq.XElement>是更简单的编程模型。</xref:System.Xml.Linq.XElement>  
  
 <xref:System.Xml.Linq.XDocument>派生自<xref:System.Xml.Linq.XContainer>。</xref:System.Xml.Linq.XContainer></xref:System.Xml.Linq.XDocument> 因此，它可以包含子节点。 但是，<xref:System.Xml.Linq.XDocument>对象只能有一个子<xref:System.Xml.Linq.XElement>节点。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> 这反映了 XML 标准，即在 XML 文档中只能有一个根元素。  
  
## <a name="components-of-xdocument"></a>Xdocument 的组件  
 <xref:System.Xml.Linq.XDocument>可以包含下列元素︰</xref:System.Xml.Linq.XDocument>  
  
-   一个<xref:System.Xml.Linq.XDeclaration>对象。</xref:System.Xml.Linq.XDeclaration> <xref:System.Xml.Linq.XDeclaration>使您能够指定 XML 声明的相关部分︰ XML 版本、 文档的编码和 XML 文档是否是独立。</xref:System.Xml.Linq.XDeclaration>  
  
-   一个<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement> 这是 XML 文档的根节点。  
  
-   任意数量的<xref:System.Xml.Linq.XProcessingInstruction>对象。</xref:System.Xml.Linq.XProcessingInstruction> 处理指令将信息传递给处理 XML 的应用程序。  
  
-   任意数量的<xref:System.Xml.Linq.XComment>对象。</xref:System.Xml.Linq.XComment> 注释将与根元素同级。 <xref:System.Xml.Linq.XComment>对象不能为在列表中，第一个参数，因为它与 XML 文档以注释开头无效。</xref:System.Xml.Linq.XComment>  
  
-   一个<xref:System.Xml.Linq.XDocumentType>的 dtd。</xref:System.Xml.Linq.XDocumentType>  
  
 当序列化<xref:System.Xml.Linq.XDocument>，即使`XDocument.Declaration`是`null`，输出将具有 XML 声明，前提是编写器已经`Writer.Settings.OmitXmlDeclaration`设置为`false`（默认值）。</xref:System.Xml.Linq.XDocument>  
  
 默认情况下，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 将版本设置为“1.0”，将编码设置为“utf-8”。  
  
## <a name="using-xelement-without-xdocument"></a>在没有 Xdocument 的情况下使用 XElement  
 正如前面提到，<xref:System.Xml.Linq.XElement>类是中的主类[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]编程接口。</xref:System.Xml.Linq.XElement> 在很多情况下，您的应用程序不需要您创建文档。 通过使用<xref:System.Xml.Linq.XElement>类，可以创建 XML 树、 向其中添加其他 XML 树，修改 XML 树中，和保存它。</xref:System.Xml.Linq.XElement>  
  
## <a name="using-xdocument"></a>使用 XDocument  
 若要构造<xref:System.Xml.Linq.XDocument>，使用函数构造，像您那样来构造<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument>  
  
 下面的代码创建<xref:System.Xml.Linq.XDocument>对象及其关联的包含对象。</xref:System.Xml.Linq.XDocument>  
  
```vb  
Dim doc As XDocument = <?xml version="1.0" encoding="utf-8"?>  
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
doc.Save("test.xml")  
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
  
## <a name="see-also"></a>另请参阅  
 [LINQ to XML 编程概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
