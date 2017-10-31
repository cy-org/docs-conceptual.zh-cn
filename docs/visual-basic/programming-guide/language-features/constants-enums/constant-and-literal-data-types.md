---
title: "常量和 Literal 数据类型 (Visual Basic) |Microsoft 文档"
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
- declaring constants, literal data types
- data types [Visual Basic], declaring
- constants, declaring
- explicit declarations
- literals, coercing data type
- declarations, data types
ms.assetid: 057206d2-3a5b-40b9-b3af-57446f9b52fa
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
ms.openlocfilehash: 22ad31415ab560b7fd0180a6dadd6d2dcd7ec77a
ms.lasthandoff: 03/13/2017

---
# <a name="constant-and-literal-data-types-visual-basic"></a>常量和 Literal 数据类型 (Visual Basic)
文本是一个值，表示为本身而不是变量的值或表达式，如数字 3 或字符串"Hello"的结果。 常量是有意义的名称，取代了文字，但它保留在整个程序，而不是一个变量，其值可能会更改此相同的值。  
  
 当[Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md)是`Off`和[Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)是`On`，您必须显式声明的所有常量具有数据类型。 在下面的示例中的数据类型`MyByte`显式声明数据类型为`Byte`:  
  
 [!code-vb[VbVbalrConstants #&1;](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/constant-and-literal-data-types_1.vb)]  
  
 当`Option Infer`是`On`或`Option Strict`是`Off`，您可以声明变量，而无需指定数据类型为`As`子句。 编译器确定的常量表达式的类型的类型。 一个数字的整数文本被强制转换到默认情况下`Integer`数据类型。 默认的数据类型为浮点数`Double`，和关键字`True`和`False`指定`Boolean`常量。  
  
## <a name="literals-and-type-coercion"></a>文本和类型强制  
 在某些情况下，您可能想要将文本强制为特定的数据类型;例如，当将特别大的整数文字值分配给类型的变量`Decimal`。 下面的示例将生成错误︰  
  
```  
Dim myDecimal as Decimal  
myDecimal = 100000000000000000000   ' This causes a compiler error.  
```  
  
 从文本表示形式会产生错误。 `Decimal`数据类型可以保存一个值过大，但文本隐式地表示为`Long`，哪些不能执行。  
  
 您可以强制转换为两种方法中的特定数据类型的文字︰ 通过将类型字符追加到它，或将它置于封闭字符内。 类型字符或封闭字符必须立即之前和/或按照在文字之前，加没有插入空格或任何类型的字符。  
  
 若要使上例正确运行，您可以将附加`D`类型，它使其表示为文本字符`Decimal`:  
  
 [!code-vb[VbVbalrConstants #&2;](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/constant-and-literal-data-types_2.vb)]  
  
 下面的示例演示类型的字符和封闭字符的正确用法︰  
  
 [!code-vb[VbVbalrConstants #&3;](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/constant-and-literal-data-types_3.vb)]  
  
 如下表所示的封闭字符和类型的字符位于[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
|数据类型|封闭字符|追加的类型字符|  
|---|---|---|  
|`Boolean`|（无）|（无）|  
|`Byte`|（无）|（无）|  
|`Char`|"|C|  
|`Date`|#|（无）|  
|`Decimal`|（无）|D 或 @|  
|`Double`|（无）|R 或 #|  
|`Integer`|（无）|I 或 %|  
|`Long`|（无）|L 或.|  
|`Short`|（无）|S|  
|`Single`|（无）|F 或 ！|  
|`String`|"|（无）|  
  
## <a name="see-also"></a>另请参阅  
 [用户定义的常量](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)   
 [如何︰ 声明常量](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)   
 [常量概述](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Option Explicit 语句](../../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [枚举概述](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [如何︰ 声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)
