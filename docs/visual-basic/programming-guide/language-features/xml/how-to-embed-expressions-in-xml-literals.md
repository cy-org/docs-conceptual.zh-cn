---
title: "如何︰ 在 XML 文本 (Visual Basic 中) 中嵌入表达式 |Microsoft 文档"
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
- embedded expressions [Visual Basic]
- XML literals [Visual Basic], embedded expressions
ms.assetid: 75016fad-0141-42de-8564-5051be29487e
caps.latest.revision: 16
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
ms.openlocfilehash: 40b0e4273223093262bc54a2b13d28fc93a44c69
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-embed-expressions-in-xml-literals-visual-basic"></a>如何：在 XML 文本中嵌入表达式 (Visual Basic)
您可以使用嵌入式表达式来创建 XML 文档、 片段或包含在运行时创建的内容的元素组合 XML 文本。 下面的示例演示如何使用嵌入式的表达式可以在运行时填充元素内容、 属性和元素名称。  
  
 嵌入式表达式的语法是`<%=` `exp` `%>`，这是相同的语法，[!INCLUDE[vstecasp](../../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)]使用。 有关详细信息，请参阅[XML 中的嵌入式表达式](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)。  
  
 您还可以使用[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]Api 来创建[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]对象。 有关详细信息，请参阅<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement>  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-insert-text-as-element-content"></a>若要作为元素内容中插入文本  
  
-   下面的示例演示如何插入中包含的文本`contactName`变量之间打开和关闭名称元素。  
  
     [!code-vb[VbXMLSamples #&39;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-embed-expressions-in-xml-literals_1.vb)]  
  
     该示例产生下面的输出：  
  
    ```  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-as-an-attribute-value"></a>若要插入文本作为属性值  
  
-   下面的示例演示如何插入中包含的文本`phoneType`变量的值作为`type`属性。  
  
     [!code-vb[VbXMLSamples #&40;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-embed-expressions-in-xml-literals_2.vb)]  
  
     该示例产生下面的输出：  
  
    ```  
    <contact>  
      <phone type="home">206-555-0144</phone>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-for-an-element-name"></a>若要插入的元素名的文本  
  
-   下面的示例演示如何插入中包含的文本`elementName`变量作为一个元素的名称。  
  
     创建元素时通过使用此技术，您必须将它们与\</&1;> 标记。  
  
     [!code-vb[VbXMLSamples #&41;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-embed-expressions-in-xml-literals_3.vb)]  
  
     该示例产生下面的输出：  
  
    ```  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [如何︰ 创建 XML 文本](../../../../visual-basic/programming-guide/language-features/xml/how-to-create-xml-literals.md)   
 [XML 中的嵌入式的表达式](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
