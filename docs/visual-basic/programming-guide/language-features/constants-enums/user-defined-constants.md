---
title: "用户定义的常量 (Visual Basic) |Microsoft 文档"
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
- constants, circular references
- Const statement [Visual Basic], user-defined constants
- user-defined constants
- scope, constants
- constants, user-defined
- circular references between constants
ms.assetid: a1206d5c-c45e-4ac2-970a-4a0be6a05fdd
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
ms.openlocfilehash: e5942d8663a8866b2f9794a86756f2bf25660ba5
ms.lasthandoff: 03/13/2017

---
# <a name="user-defined-constants-visual-basic"></a>用户定义的常量 (Visual Basic)
常量是有意义的名称，取代了数字或字符串，它不会更改。 常数存储，如名称所示，保持不变的应用程序的执行中的值。 您可以使用由该控件或您使用的组件定义的常量或可以创建您自己。 创建您自己的常数称作*用户定义*。  
  
 声明常量`Const`语句，但创建的变量名中使用相同的规则。 如果`Option Strict`是`On`，所以必须显式声明常量的类型。  
  
## <a name="const-statement-usage"></a>Const 语句使用情况  
 一个`Const`语句可以表示数学或日期/时间数量︰  
  
 [!code-vb[VbEnumsTask #&10;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_1.vb)]  
  
 它还可以定义`String`常量︰  
  
 [!code-vb[VbEnumsTask #&13;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_2.vb)]  
  
 等号右侧的表达式 ( `=` ) 通常是一个数字或文本字符串，但也可以是 （尽管该表达式不能包含对函数的调用），结果为数字或字符串的表达式。 您甚至可以定义根据以前定义的常量的常量︰  
  
 [!code-vb[VbEnumsTask #&15;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_3.vb)]  
  
## <a name="scope-of-user-defined-constants"></a>作用域的用户定义的常量  
 一个`Const`语句的作用域是在同一位置声明的变量相同。 可以在任何通过以下方式指定作用域︰  
  
-   若要创建过程中只存在一个常量，请在该过程中声明。  
  
-   若要创建一个类中的所有过程但不是属于该模块以外的任何代码都可用的常数，请将其声明的类的声明部分。  
  
-   若要创建一个常量，它可对所有成员的程序集，但不是向外部客户端的程序集，将使用其声明`Friend`类的声明部分中的关键字。  
  
-   若要创建整个应用程序中可用的常数，声明它使用`Public`关键字在下面的声明部分类。  
  
 有关详细信息，请参阅[如何︰ 声明常量](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)。  
  
### <a name="avoiding-circular-references"></a>避免循环引用  
 由于可以依据其他常数定义常量，所以有可能无意中产生*循环*，或两个或多个常量之间的循环引用。 有两个或多个公共常量，其中每个用另一个，如以下示例所示来定义，则会出现一个周期︰  
  
 [!code-vb[VbEnumsTask #&16;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_4.vb)]  
[!code-vb[VbEnumsTask #&17;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_5.vb)]  
  
 如果发生一次，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]生成一个编译器错误。  
  
## <a name="see-also"></a>另请参阅  
 [Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md)   
 [常量和 Literal 数据类型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [常量和枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/index.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [枚举概述](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [常量概述](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [如何︰ 声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
