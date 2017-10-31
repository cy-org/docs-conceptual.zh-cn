---
title: "处理 XML 文件 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- XML comments, parsing [Visual Basic]
ms.assetid: 78a15cd0-7708-4e79-85d1-c154b7a14a8c
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
ms.openlocfilehash: 72b2832d0131adf39a37ebd9297b43fb34ea49ba
ms.lasthandoff: 03/13/2017

---
# <a name="processing-the-xml-file-visual-basic"></a>处理 XML 文件 (Visual Basic)
编译器在代码中被标记为生成文档中将生成每个构造一个 ID 字符串。 (有关如何标记您的代码的信息，请参阅[XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)。)ID 字符串唯一标识指定的构造。 处理 XML 文件的程序可以使用 ID 字符串标识对应[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]元数据/反射项。  
  
 XML 文件不是代码的分层表示形式中;它是与每个元素生成的 ID 的平面列表。  
  
 在生成 ID 字符串时，编译器将遵循以下规则︰  
  
-   在字符串中不放置任何空白。  
  
-   ID 字符串的第一部分标识的那类成员标识，与单个字符后跟冒号。 使用下面的成员类型。  
  
|字符|描述|  
|---|---|  
|N|namespace<br /><br /> 无法将文档注释添加到命名空间中，但您可以使 CREF 引用到它们，在支持的情况。|  
|T|type: `Class`, `Module`, `Interface`, `Structure`, `Enum`,`Delegate`|  
|F|字段︰`Dim`|  
|P|属性︰ `Property` （包括默认属性）|  
|M|method: `Sub`, `Function`, `Declare`,`Operator`|  
|E|事件︰`Event`|  
|!|错误字符串<br /><br /> 字符串的其余部分提供有关错误的信息。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将生成链接不能解决的错误信息。|  
  
-   第二部分`String`开始命名空间根处的项的完全限定名称。 用句点分隔的项、 其封闭类型和命名空间的名称。 如果项本身的名称包含句点，它们将取代通过数字符号 （#）。 假定没有项直接在其名称中包含数字符号。 例如的完全限定的名的`String`构造函数将`System.String.#ctor`。  
  
-   对于属性和方法，如果该方法的参数括在括号中的参数列表将遵循。 如果不有任何参数，则没有括号。 参数由逗号分隔。 编码的每个参数都直接遵循如何编码中[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]签名。  
  
## <a name="example"></a>示例  
 下面的代码演示的 ID 为类的字符串，并生成它的成员。  
  
 [!code-vb[VbVbcnXmlDocComments #&10;](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/processing-the-xml-file_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)   
 [如何：创建 XML 文档](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
