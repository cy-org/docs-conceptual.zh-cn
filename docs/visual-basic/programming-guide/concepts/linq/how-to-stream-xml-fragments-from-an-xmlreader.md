---
title: "如何︰ 从 XmlReader (Visual Basic 中) 的 XML 片段进行流式处理 |Microsoft 文档"
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
ms.assetid: f67ce598-4a12-4dcb-9a07-24deca02a111
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c9c60bb4730ef6569390f76f63c40a2cbd1c9524
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-visual-basic"></a>如何︰ 从 XmlReader (Visual Basic 中) 的 XML 片段进行流式处理
如果必须处理很大的 XML 文件，将整个 XML 树加载到内存可能不可行。 本主题演示如何使用<xref:System.Xml.XmlReader>。</xref:System.Xml.XmlReader>片段进行流式处理  
  
 若要使用的最有效方法之一<xref:System.Xml.XmlReader>读取<xref:System.Xml.Linq.XElement>对象是编写您自己的自定义轴方法。</xref:System.Xml.Linq.XElement> </xref:System.Xml.XmlReader> 轴方法通常返回一个集合比如<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>，本主题中的示例中所示。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 在自定义轴方法中，通过调用创建的 XML 片段后<xref:System.Xml.Linq.XNode.ReadFrom%2A>方法，返回集合使用`yield return`。</xref:System.Xml.Linq.XNode.ReadFrom%2A> 这可为您的自定义轴方法提供延迟执行语义。  
  
 当创建 XML 树从<xref:System.Xml.XmlReader>对象，<xref:System.Xml.XmlReader>必须定位在元素上。</xref:System.Xml.XmlReader> </xref:System.Xml.XmlReader> <xref:System.Xml.Linq.XNode.ReadFrom%2A>方法不返回读取的元素结束标记之前。</xref:System.Xml.Linq.XNode.ReadFrom%2A>  
  
 如果您想要创建一个部分树，您可以实例化<xref:System.Xml.XmlReader>，将读取器定位在想要转换为节点<xref:System.Xml.Linq.XElement>树，然后再创建<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement> </xref:System.Xml.XmlReader>  
  
 主题[如何︰ 流处理可访问标头信息 (Visual Basic 中) 的 XML 片段](../../../../visual-basic/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md)包含信息以及有关如何流式处理更复杂文档的示例。  
  
 主题[如何︰ 执行流式处理转换的大型 XML 文档 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/how-to-perform-streaming-transform-of-large-xml-documents.md)包含举例说明如何使用 LINQ to XML 在保持很小的内存需求量的同时转换极大的 XML 文档。  
  
## <a name="example"></a>示例  
 本示例创建一个自定义轴方法。 可以通过使用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询来查询该方法。 自定义轴方法 `StreamRootChildDoc` 是一个专门设计的方法，用于读取具有重复 `Child` 元素的文档。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 该示例产生下面的输出：  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 在本示例中，源文档非常小。 但是即使有数百万个 `Child` 元素，本示例也仍具有很小的内存需求量。  
  
## <a name="see-also"></a>另请参阅  
 [演练︰ 在 Visual Basic 中实现 IEnumerable(Of T)](../../../../visual-basic/programming-guide/language-features/control-flow/walkthrough-implementing-ienumerable-of-t.md)   
 [分析 XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
