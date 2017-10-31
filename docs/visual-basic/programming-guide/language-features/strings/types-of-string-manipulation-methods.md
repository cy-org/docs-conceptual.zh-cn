---
title: "在 Visual Basic 中的字符串操作方法的类型 |Microsoft 文档"
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
- strings [Visual Basic], manipulating [Visual Basic]
- string manipulation
ms.assetid: 905055cd-7f50-48fb-9eed-b0995af1dc1f
caps.latest.revision: 12
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
ms.openlocfilehash: 349cfdb3e31225f6aeba90ac29aa1c66e37c7e11
ms.lasthandoff: 03/13/2017

---
# <a name="types-of-string-manipulation-methods-in-visual-basic"></a>字符串操作方法的类型 (Visual Basic)
有多种不同的方式来分析和操作字符串。 一些方法属于的[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]语言中，而其他一些固有的`String`类。  
  
## <a name="visual-basic-language-and-the-net-framework"></a>Visual Basic 语言和.NET Framework  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]为该语言的固有函数使用方法。 它们可能无需限定即可在代码中使用。 下面的示例演示的典型用法[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]字符串操作命令︰  
  
 [!code-vb[VbVbalrStrings #&44;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/types-of-string-manipulation-methods_1.vb)]  
  
 在此示例中，`Mid`函数对执行直接操作`aString`并将该值赋给`bString`。  
  
 Visual Basic 字符串操作方法的列表，请参阅[字符串操作摘要](../../../../visual-basic/language-reference/keywords/string-manipulation-summary.md)。  
  
### <a name="shared-methods-and-instance-methods"></a>共享的方法和实例方法  
 您还可以使用的方法的操作字符串`String`类。 有两种类型中的方法`String`:*共享*方法和*实例*方法。  
  
#### <a name="shared-methods"></a>共享的方法  
 共享的方法是一种方法起源于`String`类本身并不需要此类工作的实例。 这些方法可以使用的类名称限定 (`String`) 而不是与实例`String`类。 例如:   
  
 [!code-vb[VbVbalrStrings #&45;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/types-of-string-manipulation-methods_2.vb)]  
  
 在前面的示例中，<xref:System.String.Copy%2A?displayProperty=fullName>方法是静态方法，对表达式的行为被授权者提供，并且生成将值分配给`bString`。</xref:System.String.Copy%2A?displayProperty=fullName>  
  
#### <a name="instance-methods"></a>实例方法  
 实例方法，与此相反，源于的特定实例`String`并且必须具有实例名称进行限定。 例如：  
  
 [!code-vb[VbVbalrStrings #&46;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/types-of-string-manipulation-methods_3.vb)]  
  
 在此示例中，<xref:System.String.Substring%2A?displayProperty=fullName>方法是一种方法的实例的`String`(即， `aString`)。</xref:System.String.Substring%2A?displayProperty=fullName> 它对执行某项操作`aString`并将该值赋予`bString`。  
  
 有关详细信息，请参阅的文档<xref:System.String>类。</xref:System.String>  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中字符串的简介](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
