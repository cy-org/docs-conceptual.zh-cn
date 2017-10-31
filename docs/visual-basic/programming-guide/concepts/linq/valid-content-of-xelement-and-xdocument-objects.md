---
title: "有效内容的 XElement 和 XDocument Objects2 |Microsoft 文档"
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
ms.assetid: 400bb692-478a-40b6-ac1b-4ccbb4cbbd02
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f752ae346167709b95e758d15c1785ba7b6fcc5f
ms.lasthandoff: 03/13/2017

---
# <a name="valid-content-of-xelement-and-xdocument-objects"></a>XElement 和 XDocument 对象的有效内容
本主题描述可以传递给构造函数以及用于向元素和文档添加内容的方法的有效参数。  
  
## <a name="valid-content"></a>有效内容  
 查询计算的结果通常<xref:System.Collections.Generic.IEnumerable%601>或<xref:System.Xml.Linq.XElement><xref:System.Collections.Generic.IEnumerable%601><xref:System.Xml.Linq.XAttribute>。</xref:System.Xml.Linq.XAttribute>的</xref:System.Collections.Generic.IEnumerable%601></xref:System.Xml.Linq.XElement></xref:System.Collections.Generic.IEnumerable%601> 可以传递的集合<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XAttribute>对象添加到<xref:System.Xml.Linq.XElement>构造函数。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> 所以，可以很方便地将查询的结果作为内容，传递给用于填充 XML 树的方法和构造函数。  
  
 添加简单内容时，可以将多种类型传递给此方法。 有效类型包括：  
  
-   <xref:System.String></xref:System.String>  
  
-   <xref:System.Double></xref:System.Double>  
  
-   <xref:System.Single></xref:System.Single>  
  
-   <xref:System.Decimal></xref:System.Decimal>  
  
-   <xref:System.Boolean></xref:System.Boolean>  
  
-   <xref:System.DateTime></xref:System.DateTime>  
  
-   <xref:System.TimeSpan></xref:System.TimeSpan>  
  
-   <xref:System.DateTimeOffset></xref:System.DateTimeOffset>  
  
-   实现 `Object.ToString` 的任何类型。  
  
-   实现<xref:System.Collections.Generic.IEnumerable%601>。</xref:System.Collections.Generic.IEnumerable%601>的任何类型  
  
 添加复杂内容时，可以将多种类型传递给此方法：  
  
-   <xref:System.Xml.Linq.XObject></xref:System.Xml.Linq.XObject>  
  
-   <xref:System.Xml.Linq.XNode></xref:System.Xml.Linq.XNode>  
  
-   <xref:System.Xml.Linq.XAttribute>  
  
-   实现的任何类型<xref:System.Collections.Generic.IEnumerable%601></xref:System.Collections.Generic.IEnumerable%601>  
  
 如果对象实现<xref:System.Collections.Generic.IEnumerable%601>，枚举中对象的集合，并添加集合中的所有项。</xref:System.Collections.Generic.IEnumerable%601> 如果集合包含<xref:System.Xml.Linq.XNode>或<xref:System.Xml.Linq.XAttribute>对象，则单独添加集合中的每个项。</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XNode> 如果集合包含文本（或转换成文本的对象），则集合中的文本是串联在一起的，并作为单个文本节点添加。  
  
 如果内容为 `null`，则不添加任何内容。 传递集合时，集合中的项可以为 `null`。 集合中的 `null` 项对树没有任何影响。  
  
 添加的属性必须在其包含元素内具有唯一名称。  
  
 添加时<xref:System.Xml.Linq.XNode>或<xref:System.Xml.Linq.XAttribute>对象时，如果新内容没有父级，则对象简单地附加到 XML 树。</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XNode> 如果新内容已经有父级，并且是另一 XML 树的一部分，则克隆新内容，并将新克隆的内容附加到 XML 树。  
  
## <a name="valid-content-for-documents"></a>文档的有效内容  
 属性和简单内容无法添加到文档。  
  
 不需要您创建<xref:System.Xml.Linq.XDocument>。</xref:System.Xml.Linq.XDocument>的许多方案 相反，您通常可以创建 XML 树与<xref:System.Xml.Linq.XElement>根节点。</xref:System.Xml.Linq.XElement> 除非有特定要求创建文档 （例如，因为您必须在顶级创建处理指令和注释，或者必须支持文档类型），通常会更方便地使用<xref:System.Xml.Linq.XElement>作为根节点。</xref:System.Xml.Linq.XElement>  
  
 文档的有效内容包括：  
  
-   零个或一个<xref:System.Xml.Linq.XDocumentType>对象。</xref:System.Xml.Linq.XDocumentType> 文档类型必须在元素之前。  
  
-   零个或一个元素。  
  
-   零个或多个注释。  
  
-   零个或多个处理指令。  
  
-   零个或多个仅包含空白的文本节点。  
  
## <a name="constructors-and-functions-that-allow-adding-content"></a>允许添加内容的构造函数和函数  
 下面的方法允许您将子内容添加到<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XDocument>::</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
|方法|说明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.%23ctor%2A></xref:System.Xml.Linq.XElement.%23ctor%2A>|构造<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement>|  
|<xref:System.Xml.Linq.XDocument.%23ctor%2A></xref:System.Xml.Linq.XDocument.%23ctor%2A>|构造<xref:System.Xml.Linq.XDocument>。</xref:System.Xml.Linq.XDocument>|  
|<xref:System.Xml.Linq.XContainer.Add%2A></xref:System.Xml.Linq.XContainer.Add%2A>|<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XDocument>.</xref:System.Xml.Linq.XDocument></xref:System.Xml.Linq.XElement>的子内容的末尾添加|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A></xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|在<xref:System.Xml.Linq.XNode>。</xref:System.Xml.Linq.XNode>之后添加内容|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A></xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|<xref:System.Xml.Linq.XNode>。</xref:System.Xml.Linq.XNode>之前添加的内容|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A></xref:System.Xml.Linq.XContainer.AddFirst%2A>|<xref:System.Xml.Linq.XContainer>。</xref:System.Xml.Linq.XContainer>的子内容的开头添加内容|  
|<xref:System.Xml.Linq.XElement.ReplaceAll%2A></xref:System.Xml.Linq.XElement.ReplaceAll%2A>|替换<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement>的所有内容 （子节点和属性）|  
|<xref:System.Xml.Linq.XElement.ReplaceAttributes%2A></xref:System.Xml.Linq.XElement.ReplaceAttributes%2A>|替换<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement>的属性|  
|<xref:System.Xml.Linq.XContainer.ReplaceNodes%2A></xref:System.Xml.Linq.XContainer.ReplaceNodes%2A>|用新内容替换子节点。|  
|<xref:System.Xml.Linq.XNode.ReplaceWith%2A></xref:System.Xml.Linq.XNode.ReplaceWith%2A>|用新内容替换节点。|  
  
## <a name="see-also"></a>另请参阅  
 [创建 XML 树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
