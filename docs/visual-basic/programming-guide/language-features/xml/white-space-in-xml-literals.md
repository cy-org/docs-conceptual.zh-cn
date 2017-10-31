---
title: "XML 文本 (Visual Basic 中) 中的空白区域 |Microsoft 文档"
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
- white space [XML in Visual Basic]
- XML literals [Visual Basic], white space
ms.assetid: dfe3a9ff-d69a-418e-a6b5-476f4ed84219
caps.latest.revision: 14
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
ms.openlocfilehash: b98a88696f24cc0b95401812471d13acea4faa6d
ms.lasthandoff: 03/13/2017

---
# <a name="white-space-in-xml-literals-visual-basic"></a>XML 文本中的空白 (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器在其创建时包含有意义的空白字符将从 XML 文本[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]对象。 它不会合并无意义的空白字符。  
  
## <a name="significant-and-insignificant-white-space"></a>有效空白和无关紧要的空白区域  
 XML 文本中的空白字符只有三个区域中有意义︰  
  
-   当它们都在某一属性值。  
  
-   当它们都属于某个元素的文本内容，并且文本还包含其他字符。  
  
-   在嵌入式表达式中的元素的文本内容。  
  
 否则为编译器将视为无意义的空白字符，不会将它们包含在[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]文本对象。  
  
 若要在 XML 文本中包括无关紧要的空白区域，使用嵌入式的表达式，其中包含具有空白区域的字符串文本。  
  
> [!NOTE]
>  如果`xml:space`特性出现在 XML 元素文本，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器该特性包含在<xref:System.Xml.Linq.XElement>对象，但添加此属性不会更改编译器如何处理空白区域。</xref:System.Xml.Linq.XElement>  
  
## <a name="examples"></a>示例  
 下面的示例包含两个 XML 元素，但是外部和内部。 这两个元素包含文本内容中的空白区域。 外部元素中的空白区域是无意义，因为它仅包含空白区域和一个 XML 元素。 内部元素中的空白区域很重要，因为它包含的空白区域和文本。  
  
 [!code-vb[VbXMLSamples #&29;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/white-space-in-xml-literals_1.vb)]  
  
 当运行时，此代码将显示以下文本。  
  
```  
<outer>  
  <inner>  
                                          Inner text  
                                      </inner>  
</outer>  
```  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
