---
title: "XML 处理指令文本 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlLiteralProcessingInstruction
dev_langs:
- VB
helpviewer_keywords:
- XML literals [Visual Basic], processing instruction
- XML processing instruction literal [Visual Basic]
- processing instruction literal [Visual Basic]
ms.assetid: cef4f7f8-0011-4f64-8602-795077ad4f15
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
ms.openlocfilehash: 2903297fa22cd8dc10bc4b12abaa754d4f6284f2
ms.lasthandoff: 03/13/2017

---
# <a name="xml-processing-instruction-literal-visual-basic"></a>XML 处理指令文本 (Visual Basic)
一个文字表示<xref:System.Xml.Linq.XProcessingInstruction>对象。</xref:System.Xml.Linq.XProcessingInstruction>  
  
## <a name="syntax"></a>语法  
  
```  
<?piName [ = piData ] ?>  
```  
  
## <a name="parts"></a>部件  
 `<?`  
 必需。 表示 XML 处理指令文本的开头。  
  
 `piName`  
 必需。 将命名为指示哪个应用程序处理指令的目标。 不能以"xml"或"XML"开头。  
  
 `piData`  
 可选。 字符串，它指示的目标应用程序如何`piName`应处理 XML 文档。  
  
 `?>`  
 必需。 表示处理指令的结尾。  
  
## <a name="return-value"></a>返回值  
 <xref:System.Xml.Linq.XProcessingInstruction>对象。</xref:System.Xml.Linq.XProcessingInstruction>  
  
## <a name="remarks"></a>备注  
 XML 处理指令文本指示应用程序应如何处理 XML 文档。 当应用程序加载 XML 文档时，应用程序可以检查以确定如何处理该文档的 XML 处理指令。 应用程序解释的含义`piName`和`piData`。  
  
 XML 文档文本使用类似于 XML 处理指令的语法。 有关详细信息，请参阅[XML 文档文本](../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)。  
  
> [!NOTE]
>  `piName`元素不能以字符串"xml"或"XML"开头，因为 XML 1.0 规范保留这些标识符。  
  
 可以将 XML 处理指令文本分配给一个变量，或将其包含在 XML 文档文本。  
  
> [!NOTE]
>  XML 文本可以跨多行，而无需使用行继续符。 这使您可以从 XML 文档中复制内容并将其粘贴直接到[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]程序。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将调用转换为 XML 处理指令文本<xref:System.Xml.Linq.XProcessingInstruction.%23ctor%2A>构造函数。</xref:System.Xml.Linq.XProcessingInstruction.%23ctor%2A>  
  
## <a name="example"></a>示例  
 下面的示例创建一个处理指令确定 XML 文档的样式表。  
  
 [!code-vb[VbXMLSamples #&28;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-processing-instruction-literal_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Linq.XProcessingInstruction></xref:System.Xml.Linq.XProcessingInstruction>   
 [XML 文档文本](../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
