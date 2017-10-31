---
title: "在 XML (Visual Basic 中) 中嵌入表达式 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vb.XmlEmbeddedExpression
dev_langs:
- VB
helpviewer_keywords:
- embedded expressions [Visual Basic]
- LINQ to XML [Visual Basic], embedded expressions
- XML literals [Visual Basic], embedded expressions
ms.assetid: bf2eb779-b751-4b7c-854f-9f2161482352
caps.latest.revision: 22
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
ms.openlocfilehash: e5cd40e55ec23de3ad1bb2f5f065762c893d9cb3
ms.lasthandoff: 03/13/2017

---
# <a name="embedded-expressions-in-xml-visual-basic"></a>XML 中的嵌入式表达式 (Visual Basic)
嵌入的表达式，可以创建包含在运行时计算的表达式的 XML 文本。 嵌入式表达式的语法是`<%=` `expression` `%>`，这是相同的中使用的语法[!INCLUDE[vstecasp](../../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)]。  
  
 例如，您可以创建一个 XML 元素文本，组合与文字文本内容的嵌入式的表达式。  
  
 [!code-vb[VbXMLSamples #&27;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_1.vb)]  
  
 如果`isbnNumber`包含整数 12345 和`modifiedDate`包含的日期 3/5/2006，当此代码执行时，值`book`是︰  
  
```  
<book category="fiction" isbn="12345">  
  <modifiedDate>3/5/2006</modifiedDate>  
</book>  
```  
  
## <a name="embedded-expression-location-and-validation"></a>嵌入式的表达式定位和验证  
 嵌入的表达式只能出现在 XML 文本表达式中的某些位置。 可以返回类型的表达式的表达式位置控件以及如何`Nothing`进行处理。 下表描述允许的位置和嵌入式表达式的类型。  
  
|在文本中的位置|表达式的类型|处理`Nothing`|  
|---|---|---|  
|XML 元素名称|<xref:System.Xml.Linq.XName></xref:System.Xml.Linq.XName>|错误|  
|XML 元素内容|`Object`或数组`Object`|忽略|  
|XML 元素特性名|<xref:System.Xml.Linq.XName></xref:System.Xml.Linq.XName>|错误，除非也是属性值`Nothing`|  
|XML 元素特性值|`Object`|忽略的属性声明|  
|XML 元素特性|<xref:System.Xml.Linq.XAttribute>或集合<xref:System.Xml.Linq.XAttribute></xref:System.Xml.Linq.XAttribute></xref:System.Xml.Linq.XAttribute>|忽略|  
|XML 文档根元素|<xref:System.Xml.Linq.XElement>或者一个<xref:System.Xml.Linq.XElement>对象和任意数目的<xref:System.Xml.Linq.XProcessingInstruction>和<xref:System.Xml.Linq.XComment>对象</xref:System.Xml.Linq.XComment></xref:System.Xml.Linq.XProcessingInstruction></xref:System.Xml.Linq.XElement>的集合</xref:System.Xml.Linq.XElement>|忽略|  
  
-   XML 元素名称中的嵌入式表达式的示例︰  
  
     [!code-vb[VbXMLSamples #&32;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_2.vb)]  
  
-   XML 元素内容中的嵌入式表达式的示例︰  
  
     [!code-vb[VbXMLSamples 第&33;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_3.vb)]  
  
-   XML 元素特性名称中的嵌入式表达式的示例︰  
  
     [!code-vb[VbXMLSamples #&34;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_4.vb)]  
  
-   XML 元素特性值中的嵌入式表达式的示例︰  
  
     [!code-vb[VbXMLSamples #&35;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_5.vb)]  
  
-   在 XML 元素特性中的嵌入式表达式的示例︰  
  
     [!code-vb[VbXMLSamples #&36;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_6.vb)]  
  
-   XML 文档根元素中的嵌入式表达式的示例︰  
  
     [!code-vb[VbXMLSamples #&37;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_7.vb)]  
  
 如果您启用`Option Strict`，编译器会检查每个嵌入的表达式的类型加宽到所需的类型。 唯一的例外是，代码将运行时，会验证 XML 文档的根元素。 如果您的情况下编译`Option Strict`，可以嵌入类型的表达式`Object`并在运行时验证它们的类型。  
  
 可选的内容的位置中嵌入表达式包含`Nothing`将被忽略。 这意味着无需检查元素内容、 属性值，并且数组元素不是`Nothing`使用 XML 文本之前。 所需值，例如，元素和属性名称不能为`Nothing`。  
  
 有关在特定类型的文本中使用嵌入式的表达式的详细信息，请参阅[XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)， [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)。  
  
## <a name="scoping-rules"></a>作用域规则  
 编译器将每个 XML 文本转换为相应的文本类型的构造函数调用。 文本内容和 XML 文本中嵌入的表达式作为参数传递给构造函数。 这意味着所有[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]可用于 XML 文本的编程元素也都可在其嵌入式表达式。  
  
 在 XML 文本中，可以用声明的前缀的 XML 命名空间来访问`Imports`语句。 您可以声明新的 XML 命名空间前缀，或现有的 XML 命名空间前缀，使用元素中的卷影`xmlns`属性。 新的命名空间位于该元素的子节点但不是属于 XML 文本中嵌入的表达式。  
  
> [!NOTE]
>  当使用声明 XML 命名空间前缀`xmlns`命名空间属性，属性值必须是常量字符串。 在这方面，使用`xmlns`属性是类似于使用`Imports`语句声明 XML 命名空间。 不能使用嵌入式的表达式来指定 XML 命名空间值。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [XML 文本概述](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md)
