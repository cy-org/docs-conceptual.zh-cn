---
title: "XML 文档文本 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlLiteralDocument
dev_langs:
- VB
helpviewer_keywords:
- XML document literal [Visual Basic]
- XML literals [Visual Basic], document
- XML documents [Visual Basic], creating
- document literal [Visual Basic]
ms.assetid: f7bbee56-0911-41de-b907-96f20450137b
caps.latest.revision: 20
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
ms.openlocfilehash: 5d64faddad66eba4029969654388ba7df17e5854
ms.lasthandoff: 03/13/2017

---
# <a name="xml-document-literal-visual-basic"></a>XML 文档文本 (Visual Basic)
一个文字表示<xref:System.Xml.Linq.XDocument>对象。</xref:System.Xml.Linq.XDocument>  
  
## <a name="syntax"></a>语法  
  
```  
<?xml version="1.0" [encoding="encoding"] [standalone="standalone"] ?>  
[ piCommentList ]  
rootElement  
[ piCommentList ]  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`encoding`|可选。 声明的编码的文档使用的文字文本。|  
|`standalone`|可选。 文字文本。 必须是"yes"或"no"。|  
|`piCommentList`|可选。 XML 处理指令和 XML 注释的列表。 采用以下格式︰<br /><br /> `piComment [` `piComment` `... ]`<br /><br /> 每个`piComment`可以是以下之一︰<br /><br /> -   [XML 处理指令文本](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md)。<br />-   [XML 注释文本](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md)。|  
|`rootElement`|必需。 文档的根元素。 格式为以下项之一︰<br /><br /> <ul><li>[XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)。</li><li>窗体的嵌入式表达式`<%=` `elementExp` `%>`。 `elementExp`返回以下类型之一︰<br /><br /> <ul><li><xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement></li><li>一个集合，包含一个<xref:System.Xml.Linq.XElement>对象以及任意数量的<xref:System.Xml.Linq.XProcessingInstruction>和<xref:System.Xml.Linq.XComment>对象。</xref:System.Xml.Linq.XComment> </xref:System.Xml.Linq.XProcessingInstruction> </xref:System.Xml.Linq.XElement></li></ul></li></ul><br /> 有关详细信息，请参阅[XML 中的嵌入式表达式](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)。|  
  
## <a name="return-value"></a>返回值  
 <xref:System.Xml.Linq.XDocument>对象。</xref:System.Xml.Linq.XDocument>  
  
## <a name="remarks"></a>备注  
 通过文本开头的 XML 声明进行标识的 XML 文档文本。 尽管每个 XML 文档文本必须恰好一个根 XML 元素，它可以有任意数量的 XML 处理指令和 XML 注释。  
  
 XML 文档文本不能出现在一个 XML 元素。  
  
> [!NOTE]
>  XML 文本可以跨多个行，而无需使用行继续符。 这使您可以从 XML 文档中复制内容并将其粘贴直接到[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]程序。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将 XML 文档文本转换为对调用<xref:System.Xml.Linq.XDocument.%23ctor%2A>和<xref:System.Xml.Linq.XDeclaration.%23ctor%2A>构造函数。</xref:System.Xml.Linq.XDeclaration.%23ctor%2A> </xref:System.Xml.Linq.XDocument.%23ctor%2A>  
  
## <a name="example"></a>示例  
 下面的示例创建具有 XML 声明、 处理指令、 注释和一个包含另一个元素的元素的 XML 文档。  
  
 [!code-vb[VbXMLSamples #&30;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-document-literal_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Linq.XElement>   
 <xref:System.Xml.Linq.XProcessingInstruction></xref:System.Xml.Linq.XProcessingInstruction>   
 <xref:System.Xml.Linq.XComment></xref:System.Xml.Linq.XComment>   
 <xref:System.Xml.Linq.XDocument></xref:System.Xml.Linq.XDocument>   
 [XML 处理指令文本](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md)   
 [XML 注释文本](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md)   
 [XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 中的嵌入式表达式](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)
