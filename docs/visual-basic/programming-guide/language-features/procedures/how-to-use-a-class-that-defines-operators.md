---
title: "如何︰ 使用类定义的运算符 (Visual Basic 中) |Microsoft 文档"
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
- operator procedures, calling
- procedures, operator
- procedures, calling
- examples [Visual Basic], CType
- syntax, Operator procedures
- operators [Visual Basic], overloading
- return values, Operator procedures
- operator overloading
ms.assetid: 7ccce94a-6ca0-47d1-9f3f-13385d34f5d5
caps.latest.revision: 21
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
ms.openlocfilehash: b1db7c0b2a6fd8160baa48892b5f2214df24674e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-use-a-class-that-defines-operators-visual-basic"></a>如何：使用定义运算符的类 (Visual Basic)
如果使用类或结构，它定义自己的运算符，您可以访问这些运算符从[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
 也称为上类或结构定义一个运算符*重载*运算符。  
  
## <a name="example"></a>示例  
 以下示例将访问 SQL 结构<xref:System.Data.SqlTypes.SqlString>，它定义转换运算符 ([CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)) 中的 SQL 字符串之间进行双向和[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]字符串。</xref:System.Data.SqlTypes.SqlString> 使用`CType(` *SQL 字符串表达式*， `String)` SQL 将字符串转换为[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]字符串，并`CType(` *Visual Basic 字符串表达式*，<xref:System.Data.SqlTypes.SqlString>`)`在反向转换。</xref:System.Data.SqlTypes.SqlString>  
  
 [!code-vb[VbVbcnProcedures #&30;](./codesnippet/VisualBasic/how-to-use-a-class-that-defines-operators_1.vb)]  
  
 [!code-vb[VbVbcnProcedures #&31;](./codesnippet/VisualBasic/how-to-use-a-class-that-defines-operators_2.vb)]  
  
 <xref:System.Data.SqlTypes.SqlString>结构定义的转换运算符 ([CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)) 从`String`到<xref:System.Data.SqlTypes.SqlString>，另一个从<xref:System.Data.SqlTypes.SqlString>到`String`。</xref:System.Data.SqlTypes.SqlString> </xref:System.Data.SqlTypes.SqlString> </xref:System.Data.SqlTypes.SqlString> 将分配的语句`title`到`jobTitle`利用了第一个运算符，与<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>函数调用时，使用第二个。</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
  
## <a name="compiling-the-code"></a>编译代码  
 请确保类或结构正在使用定义你想要使用的运算符。 不要假定类或结构已定义每个运算符可进行重载。 可用运算符的列表，请参阅[Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)。  
  
 包括相应`Imports`SQL 字符串的开头的源文件的语句 (在这种情况下<xref:System.Data.SqlTypes>)。</xref:System.Data.SqlTypes>  
  
 您的项目必须具有对 System.Data 和 System.XML 的引用。  
  
## <a name="see-also"></a>另请参阅  
 [运算符过程](./operator-procedures.md)   
 [如何︰ 定义运算符](./how-to-define-an-operator.md)   
 [如何︰ 定义转换运算符](./how-to-define-a-conversion-operator.md)   
 [如何︰ 调用运算符过程](./how-to-call-an-operator-procedure.md)   
 [扩大转换](../../../../visual-basic/language-reference/modifiers/widening.md)   
 [收缩转换](../../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [如何︰ 声明结构](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [隐式和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
