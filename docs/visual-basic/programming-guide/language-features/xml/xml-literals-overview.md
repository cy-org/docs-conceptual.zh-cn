---
title: "XML 文本概述 (Visual Basic 中) |Microsoft 文档"
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
helpviewer_keywords:
- XML literals [Visual Basic], about XML literals
- declaring XML literals [Visual Basic]
- LINQ to XML [Visual Basic], XML literals
- literals [Visual Basic], XML
ms.assetid: 37987c15-4ab8-471b-bd45-399816bfb57f
caps.latest.revision: 27
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 57d036910ba9e49385caca28de222a8a8e28ec56
ms.lasthandoff: 03/13/2017

---
# <a name="xml-literals-overview-visual-basic"></a>XML 文本概述 (Visual Basic)
*XML 文本*允许您将并入 XML 直接插入到您[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]代码。 XML 文本语法表示[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]对象，也是如此类似于 XML 1.0 语法。 这使得更轻松地以编程方式创建 XML 元素和文档，因为您的代码具有相同的结构与最终的 XML。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将为 XML 文字编译[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]对象。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]提供用于创建和操作 XML 的简单对象模型和此模型也与集成[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]。 有关详细信息，请参阅<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement>  
  
 您可以将嵌入[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]XML 文本中的表达式。 在运行时，应用程序创建[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]每个文本包含嵌入的表达式的值的对象。 这允许您指定在 XML 文本的动态内容。 有关详细信息，请参阅[XML 中的嵌入式表达式](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)。  
  
 关于 XML 文本语法和 XML 1.0 语法之间的差异的详细信息，请参阅[XML 文本和 XML 1.0 规范](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md)。  
  
## <a name="simple-literals"></a>简单的文本  
 您可以创建[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]对象在您[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]通过键入或粘贴有效的 xml 代码。 XML 元素文本返回<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement> 有关详细信息，请参阅[XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)和[XML 文本和 XML 1.0 规范](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md)。 下面的示例创建具有多个子元素的 XML 元素。  
  
 [!code-vb[VbXMLSamples #&5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_1.vb)]  
  
 可以通过启动 XML 文本与创建的 XML 文档`<?xml version="1.0"?>`，如在下面的示例所示。 返回的 XML 文档文本<xref:System.Xml.Linq.XDocument>对象。</xref:System.Xml.Linq.XDocument> 有关详细信息，请参阅[XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)。  
  
 [!code-vb[VbXMLSamples #&6;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_2.vb)]  
  
> [!NOTE]
>  中的 XML 文本语法[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不等同于 XML 1.0 规范中的语法。 有关详细信息，请参阅[XML 文本和 XML 1.0 规范](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md)。  
  
## <a name="line-continuation"></a>行继续符  
 XML 文本可以跨多个行，而无需使用行继续符 （空格下划线回车序列）。 这使得更轻松地比较 XML 文档的代码中的 XML 文本。  
  
 作为 XML 文本的一部分，则编译器将行继续符。 因此，应使用空格下划线回车序列仅在它属于时[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]对象。  
  
 但是，如果嵌入式表达式中有多行的表达式需要行继续符。 有关详细信息，请参阅[XML 中的嵌入式表达式](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)。  
  
## <a name="embedding-queries-in-xml-literals"></a>在 XML 文本中嵌入的查询  
 可以在嵌入式表达式中使用查询。 执行此操作时，由查询返回的元素添加到的 XML 元素。 这允许您添加到 XML 文本的动态内容，例如用户查询的结果。  
  
 例如，下面的代码使用嵌入式的查询从的成员创建的 XML 元素`phoneNumbers2`数组，然后将这些元素添加子级为`contact2`。  
  
 [!code-vb[VbXMLSamples #&7;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_3.vb)]  
  
## <a name="how-the-compiler-creates-objects-from-xml-literals"></a>从 XML 文本，编译器如何创建对象  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将 XML 文本转换为等效的调用[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]构造函数来构建[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]对象。 例如，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器会将下面的代码示例转换为调用<xref:System.Xml.Linq.XProcessingInstruction>XML 版本指令，构造函数调用到<xref:System.Xml.Linq.XElement>构造函数`<contact>`， `<name>`，和`<phone>`元素和对调用<xref:System.Xml.Linq.XAttribute>构造函数`type`属性。</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XProcessingInstruction> 具体而言，在下面的示例中，提供的属性[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将调用<xref:System.Xml.Linq.XAttribute.%23ctor%28System.Xml.Linq.XName%2CSystem.Object%29>构造函数两次。</xref:System.Xml.Linq.XAttribute.%23ctor%28System.Xml.Linq.XName%2CSystem.Object%29> 第一个将值传递`type`为`name`参数和值`home`为`value`参数。 第二个还传递值`type`为`name`参数，但值`work`为`value`参数。  
  
 [!code-vb[VbXMLSamples #&6;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Linq.XElement>   
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 中的嵌入式的表达式](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 文本](../../../../visual-basic/language-reference/xml-literals/index.md)
