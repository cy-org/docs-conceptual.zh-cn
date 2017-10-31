---
title: "何时使用枚举 (Visual Basic 中) |Microsoft 文档"
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
- enumerations [Visual Basic]
ms.assetid: e6e47b5b-3ed9-452d-a481-9c3fed88519a
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
ms.openlocfilehash: f22102a2e1e7eafd7fcf4db1f46af2cc622eba70
ms.lasthandoff: 03/13/2017

---
# <a name="when-to-use-an-enumeration-visual-basic"></a>何时使用枚举 (Visual Basic)
枚举提供了使用成组相关的常数的一个简单的办法。 一个枚举，或`Enum`，是一组值的符号名称。 枚举被视为数据类型，并可用于创建具有变量和属性的使用的常数的集。  
  
## <a name="when-to-use-an-enumeration"></a>何时使用枚举  
 当一个过程接受一组有限的变量时，请考虑使用枚举。 枚举可使更清晰且更具可读性的代码，特别是当使用有意义的名称。  
  
 使用枚举的好处包括︰  
  
-   这样可以减少错误引起的转置或键入数字。  
  
-   便于在以后更改值。  
  
-   使代码易于阅读，这意味着它不太可能错误的概率到其中。  
  
-   确保向前兼容性。 借助枚举、 您的代码就很难，如果有人在将来更改的成员名称所对应的值失败。  
  
## <a name="naming-enumerations"></a>命名的枚举  
 使用枚举成员的命名约定。 当[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]遇到枚举成员名称，如果其他引用的类型库包含相同的名称，可能会引发异常。 使用唯一的前缀，用于标识您的应用程序或组件中的值。  
  
 当引用时枚举的成员，必须限定成员名称为枚举名称，否则使用`Imports`语句。 有关详细信息，请参阅[枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)。  
  
## <a name="predefined-enumerations"></a>预定义的枚举  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供的预定义的枚举数，如`FirstDayOfWeek`和`MsgBoxResul`t，以便于您的代码。 这些因素的列表，请参阅[常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何︰ 声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [如何︰ 为枚举成员，请参阅](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [如何︰ 循环访问在 Visual Basic 中枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [如何︰ 确定与枚举值关联的字符串](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [Enum 语句](../../../../visual-basic/language-reference/statements/enum-statement.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)
