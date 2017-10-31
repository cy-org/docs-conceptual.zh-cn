---
title: "Visual Basic 中的数据类型"
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
- data types [Visual Basic], declaring
- typing
- data types [Visual Basic]
- Visual Basic code, data types
- data types [Visual Basic], improving speed with
ms.assetid: 5e1b9aaf-c7ca-4b29-9b22-0e82ed8e85e2
caps.latest.revision: 28
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8b90a5e58d135a3769761ca431fd0c05f79e045f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="data-types-in-visual-basic"></a>Visual Basic 中的数据类型
编程元素的*数据类型*是指可以保留的数据种类以及相应类型数据的存储方式。 数据类型适用于所有可以存储到计算机内存中或参与表达式求值的值。 每个变量、文本、常量、枚举、属性、过程参数、过程自变量和过程返回值都有对应的数据类型。  
  
## <a name="declared-data-types"></a>已声明的数据类型  
 可以使用声明语句定义编程元素，并使用 `As` 子句指定其数据类型。 下表列出了用于声明各种元素的语句。  
  
|编程元素|数据类型声明|  
|-------------------------|---------------------------|  
|变量|使用 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)<br /><br /> `Dim`   `amount As Double`<br /><br /> `Static`   `yourName As String`<br /><br /> `Public`   `billsPaid As Decimal = 0`|  
|Literal|含文本类型字符；请参阅[类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)中的“文本类型字符”<br /><br /> `Dim searchChar As Char = "."`  `C`|  
|常量|使用 [Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md)<br /><br /> `Const`   `modulus As Single = 4.17825F`|  
|枚举|使用 [Enum 语句](../../../../visual-basic/language-reference/statements/enum-statement.md)<br /><br /> `Public`   `Enum`   `colors`|  
|属性|使用 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)<br /><br /> `Property`   `region() As String`|  
|过程参数|使用 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)、[Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)或 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)<br /><br /> `Sub addSale(ByVal`   `amount`   `As Double)`|  
|过程自变量|在调用的代码中；每个自变量都是一个已声明的编程元素或包含已声明元素的表达式<br /><br /> `subString = Left(`  `inputString`  `,`   `5`  `)`|  
|过程返回值|使用 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)或 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)<br /><br /> `Function convert(ByVal b As Byte)`   `As String`|  
  
 有关 Visual Basic 数据类型的列表，请参阅[数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)。  
  
## <a name="see-also"></a>另请参阅  
 [类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [元组](tuples.md)     
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [有效使用数据类型](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)

