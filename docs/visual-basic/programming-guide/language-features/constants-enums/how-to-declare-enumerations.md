---
title: "如何︰ 声明枚举 (Visual Basic 中) |Microsoft 文档"
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
- declarations, enumerations
- enumerations [Visual Basic], declaring
- declaring enumerations
ms.assetid: db4ca1c3-f429-4c81-ae81-29e0157b29fd
caps.latest.revision: 24
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
ms.openlocfilehash: 8ff8bf2df39bed0597740bcda968283ec854f447
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-declare-enumerations-visual-basic"></a>如何：声明枚举 (Visual Basic)
创建一个包含枚举`Enum`的类或模块中的声明部分语句。 不能声明在方法内的枚举。 若要指定适当的访问级别，使用`Private`， `Protected`， `Friend`，或`Public`。  
  
 `Enum`类型都有一个名称、 一个基础类型和一组字段，各表示一个常数。 该名称必须是一个有效[!INCLUDE[vbprvblong](../../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]限定符。 基础类型必须是整数类型之一-`Byte`， `Short`，`Long`或`Integer`。 默认为 `Integer`。 枚举始终强类型和不可互换与整数类型。  
  
 枚举不能具有浮点值。 如果枚举器分配一个浮点值与`Option Strict On`，将导致编译器错误。 如果`Option Strict`是`Off`的值自动转换为`Enum`类型。  
  
 有关如何使用和信息的名称，`Imports`语句来进行名称限定不必要的请参阅[枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)。  
  
### <a name="to-declare-an-enumeration"></a>声明枚举  
  
1.  编写一个包括代码访问级别的声明`Enum`关键字和有效的名称，如下面的示例，其中每个声明一个不同`Enum`。  
  
     [!code-vb[VbEnumsTask #&3;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_1.vb)]  
  
2.  枚举中定义的常量。 默认情况下，将为枚举中的第一个常数初始化为`0`，而后面的常数将初始化为其中一个比前面的常数的值。 例如，下面的枚举， `Days`，包含一个名为常量`Sunday`值`0`，一个名为常量`Monday`值`1`，一个名为常量`Tuesday`值为`2`，依次类推。  
  
     [!code-vb[VbEnumsTask #&4;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_2.vb)]  
  
3.  可以使用赋值语句，显式枚举中常数中分配的值。 您可以分配任何整数值，包括负数。 例如，您可能想常量与值小于零，表示错误情况。 在下面的枚举常量`Invalid`显式分配的值`–1`，和常量`Sunday`的值赋给`0`。 因为它是在枚举中，第一个常量`Saturday`还初始化为值`0`。 值`Monday`是`1`(一的值大于`Sunday`); 的值`Tuesday`是`2`，依次类推。  
  
     [!code-vb[VbEnumsTask #&5;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_3.vb)]  
  
### <a name="to-declare-an-enumeration-as-an-explicit-type"></a>若要声明为显式类型枚举  
  
-   使用指定的枚举类型`As`子句，如下面的示例中所示。  
  
     [!code-vb[VbEnumsTask #&6;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_4.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [如何︰ 为枚举成员，请参阅](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [如何︰ 循环访问在 Visual Basic 中枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [如何︰ 确定与枚举值关联的字符串](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [何时使用枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)   
 [常量概述](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [常量和 Literal 数据类型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)
