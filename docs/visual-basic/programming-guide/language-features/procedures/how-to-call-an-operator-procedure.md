---
title: "如何︰ 调用运算符过程 (Visual Basic 中) |Microsoft 文档"
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
- procedure calls, operator overloading
- syntax, Operator procedures
- operators [Visual Basic], overloading
- return values, Operator procedures
- overloaded operators, calling
- operator overloading
ms.assetid: 0dce42cc-f0b0-4c14-9f62-018b21f33497
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
ms.openlocfilehash: 2403e7a8270c17a8db5417cd8394fd47c373d493
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-an-operator-procedure-visual-basic"></a>如何：调用运算符过程 (Visual Basic)
通过在表达式中使用的运算符符号调用运算符过程。 对于转换运算符，则调用[CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)将值从一种数据类型转换到另一个。  
  
 不显式调用运算符过程。 只需使用该运算符或`CType`函数，在赋值语句或表达式，通常使用的运算符相同的方式。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]在调用运算符过程。  
  
 也称为上类或结构定义一个运算符*重载*运算符。  
  
### <a name="to-call-an-operator-procedure"></a>若要调用运算符过程  
  
1.  以正常方式在表达式中使用运算符符号。  
  
2.  请确保操作数的数据类型是适合于该运算符，且按正确的顺序。  
  
3.  运算符可按预期方式的表达式值发挥作用。  
  
### <a name="to-call-a-conversion-operator-procedure"></a>若要调用的转换运算符过程  
  
1.  使用`CType`在表达式内。  
  
2.  请确保操作数的数据类型进行转换，并以正确的顺序。  
  
3.  `CType`调用转换运算符过程并返回转换后的值。  
  
## <a name="example"></a>示例  
 下面的示例创建两个<xref:System.TimeSpan>结构，并将它们相加，并将结果存储在第三个<xref:System.TimeSpan>结构。</xref:System.TimeSpan> </xref:System.TimeSpan> <xref:System.TimeSpan>结构定义运算符过程来重载了几个标准运算符。</xref:System.TimeSpan>  
  
 [!code-vb[VbVbcnProcedures #&29;](./codesnippet/VisualBasic/how-to-call-an-operator-procedure_1.vb)]  
  
 因为<xref:System.TimeSpan>重载标准`+`运算符，则在计算的值前面的示例调用运算符过程`combinedSpan`。</xref:System.TimeSpan>  
  
 调用转换运算符过程的示例，请参阅[如何︰ 使用此类定义运算符的类](./how-to-use-a-class-that-defines-operators.md)。  
  
## <a name="compiling-the-code"></a>编译代码  
 请确保类或结构正在使用定义你想要使用的运算符。  
  
## <a name="see-also"></a>请参见  
 [运算符过程](./operator-procedures.md)   
 [如何︰ 定义运算符](./how-to-define-an-operator.md)   
 [如何︰ 定义转换运算符](./how-to-define-a-conversion-operator.md)   
 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [扩大转换](../../../../visual-basic/language-reference/modifiers/widening.md)   
 [收缩转换](../../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [如何︰ 声明结构](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [隐式和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
