---
title: "在 Visual Basic 中的串联运算符 |Microsoft 文档"
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
- '& operator [Visual Basic], concatenation'
- concatenation operators
- operators [Visual Basic], concatenation
- Visual Basic code, operators
- + operator [Visual Basic], concatenation
- concatenation operators, Visual Basic strings
ms.assetid: e59908c3-89e0-41ae-933d-3e8826c16a04
caps.latest.revision: 18
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
ms.openlocfilehash: fa11f1dcff2c333861596cbac03391403cf962c1
ms.lasthandoff: 03/13/2017

---
# <a name="concatenation-operators-in-visual-basic"></a>串联运算符 (Visual Basic)
串联运算符将多个字符串联接为一个字符串。 有两种串联运算符：`+` 和 `&`。 这两种串联运算符都执行基本的串联运算，如下面的示例所示。  
  
```vb
Dim x As String = "Mic" & "ro" & "soft" 
Dim y As String = "Mic" + "ro" + "soft" 
' The preceding statements set both x and y to "Microsoft".
```  
  
 这两种运算符还可以串联 `String` 变量，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators #&76;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/concatenation-operators_1.vb)]  
  
## <a name="differences-between-the-two-concatenation-operators"></a>两种串联运算符之间的区别  
 [+ 运算符](../../../../visual-basic/language-reference/operators/addition-operator.md)具有两个数字相加的主要目的。 然而，它还可以将数值操作数与字符串操作数串联起来。 `+`运算符具有一组复杂的规则，用于确定是要添加、 串联、 指示编译器错误还是引发运行时<xref:System.InvalidCastException>异常。</xref:System.InvalidCastException>  
  
 [& 运算符](../../../../visual-basic/language-reference/operators/concatenation-operator.md)仅为定义`String`操作数，而且始终将向其操作数扩展`String`，而不考虑设置的`Option Strict`。 对于字符串串联操作，建议使用 `&` 运算符，原因是它以独占方式为字符串定义，并降低产生意外转换的可能性。  
  
## <a name="performance-string-and-stringbuilder"></a>性能：字符串和 StringBuilder  
 如果这样做很多操作在一个字符串，如串联、 删除或替换，您的性能可能会提高从<xref:System.Text.StringBuilder>类<xref:System.Text>命名空间。</xref:System.Text> </xref:System.Text.StringBuilder> 它采用额外指令来创建和初始化<xref:System.Text.StringBuilder>对象和其他指令将转换为其最终值`String`，但此时可能会因为恢复<xref:System.Text.StringBuilder>可以更快地执行。</xref:System.Text.StringBuilder> </xref:System.Text.StringBuilder>  
  
## <a name="see-also"></a>另请参阅  
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [在 Visual Basic 中的字符串操作方法的类型](../../../../visual-basic/programming-guide/language-features/strings/types-of-string-manipulation-methods.md)   
 [在 Visual Basic 中的算术运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [在 Visual Basic 中的比较运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [在 Visual Basic 中的逻辑和按位运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
