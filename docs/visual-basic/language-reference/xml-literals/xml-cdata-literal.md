---
title: "XML CDATA 文本 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlLiteralCdata
dev_langs:
- VB
helpviewer_keywords:
- CDATA literal [Visual Basic]
- XML CDATA literal [Visual Basic]
- XML literals [Visual Basic], CDATA
ms.assetid: 9eafb6a4-dd9d-4866-85e8-0654c65abc44
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
ms.openlocfilehash: 24e52bf203ff3df57e26137da24abcc2cb7e8e20
ms.lasthandoff: 03/13/2017

---
# <a name="xml-cdata-literal-visual-basic"></a>XML CDATA 文本 (Visual Basic)
一个文字表示<xref:System.Xml.Linq.XCData>对象。</xref:System.Xml.Linq.XCData>  
  
## <a name="syntax"></a>语法  
  
```  
<![CDATA[content]]>  
```  
  
## <a name="parts"></a>部件  
 `<![CDATA[`  
 必需。 表示 XML CDATA 节的开头。  
  
 `content`  
 必需。 若要显示在 XML CDATA 部分中的文本内容。  
  
 `]]>`  
 必需。 表示部分的结尾。  
  
## <a name="return-value"></a>返回值  
 <xref:System.Xml.Linq.XCData>对象。</xref:System.Xml.Linq.XCData>  
  
## <a name="remarks"></a>备注  
 XML CDATA 节包含应包含，但不是会分析，含 XML 中包含它的原始文本。 XML CDATA 部分可以包含的任何文本。 这包括 XML 保留的字符。 XML CDATA 部分结束与序列"]]&1;>"。 这意味着以下几点︰  
  
-   您不能在 XML CDATA 文本中使用嵌入式的表达式，因为嵌入式的表达式分隔符是有效的 XML CDATA 内容。  
  
-   XML CDATA 节无法嵌套，因为`content`不能包含值"]]&1;>"。  
  
 您可以将 XML CDATA 文本分配给一个变量，或将其包含在 XML 元素文本。  
  
> [!NOTE]
>  XML 文本可以跨多个行，但不使用行继续符。 这使您可以从 XML 文档中复制内容并将其粘贴直接到[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]程序。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将 XML CDATA 文本转换为调用<xref:System.Xml.Linq.XCData.%23ctor%2A>构造函数。</xref:System.Xml.Linq.XCData.%23ctor%2A>  
  
## <a name="example"></a>示例  
 下面的示例创建一个包含文本的 CDATA 节"可以包含文字\<XML&1;> 标记"。  
  
 [!code-vb[VbXMLSamples 第&23;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-cdata-literal_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Linq.XCData></xref:System.Xml.Linq.XCData>   
 [XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
