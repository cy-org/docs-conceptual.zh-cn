---
title: "XML 注释文本 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlLiteralComment
dev_langs:
- VB
helpviewer_keywords:
- comment literal [Visual Basic]
- XML comments, adding [Visual Basic]
- XML comment literal [Visual Basic]
- XML literals [Visual Basic], comment
ms.assetid: 634c1cee-5e01-48d0-88d7-2dd55e4a9e52
caps.latest.revision: 19
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
ms.openlocfilehash: 88cfb984be42345ae1e5c998cf82aa1415d2455e
ms.lasthandoff: 03/13/2017

---
# <a name="xml-comment-literal-visual-basic"></a>XML 注释文本 (Visual Basic)
一个文字表示<xref:System.Xml.Linq.XComment>对象。</xref:System.Xml.Linq.XComment>  
  
## <a name="syntax"></a>语法  
  
```  
<!-- content -->  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`<!--`|必需。 表示 XML 注释的开头。|  
|`content`|必需。 将出现在 XML 注释文本。 不能包含一系列的两个连字符 （-） 或相邻的结束标记的连字符结尾。|  
|`-->`|必需。 表示 XML 注释的结尾。|  
  
## <a name="return-value"></a>返回值  
 <xref:System.Xml.Linq.XComment>对象。</xref:System.Xml.Linq.XComment>  
  
## <a name="remarks"></a>备注  
 XML 注释文本不包含文档内容;它们包含有关文档的信息。 XML 注释部分结尾"-->"的序列。 这意味着以下几点︰  
  
-   您不能在 XML 注释文本中使用嵌入式的表达式，因为嵌入式的表达式分隔符是有效的 XML 注释内容。  
  
-   不能嵌套 XML 注释部分，因为`content`不能包含"-->"的值。  
  
 可以将 XML 注释文本分配给一个变量，或者可以将其包含在 XML 元素文本。  
  
> [!NOTE]
>  XML 文本可以跨多个行，而无需使用行继续符。 此功能允许你复制内容的 XML 文档中，将其粘贴直接到[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]程序。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将 XML 注释文本转换为调用<xref:System.Xml.Linq.XComment.%23ctor%2A>构造函数。</xref:System.Xml.Linq.XComment.%23ctor%2A>  
  
## <a name="example"></a>示例  
 下面的示例创建包含文本的 XML 注释"这是一条注释"。  
  
 [!code-vb[VbXMLSamples #&9;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-comment-literal_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Linq.XComment></xref:System.Xml.Linq.XComment>   
 [XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
