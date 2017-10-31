---
title: "有效使用数据类型 (Visual Basic 中) |Microsoft 文档"
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
- performance, data type efficiency
- data types [Visual Basic], weak typing
- AscW function, preferred to Asc
- data types [Visual Basic], using efficiently
- optimization, data types
- data types [Visual Basic], strong typing
- strong typing
- typing, strong
- data types [Visual Basic], optimizing
- ChrW function, preferred to Chr
ms.assetid: 28f5e4ba-ec24-4f37-b90a-e8ee822f778a
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
ms.openlocfilehash: b81a1c81d970beee32925c3f2fe6ca3bcad79151
ms.lasthandoff: 03/13/2017

---
# <a name="efficient-use-of-data-types-visual-basic"></a>有效使用数据类型 (Visual Basic)
未声明的变量和数据类型未声明的变量分配`Object`数据类型。 这使得更易于编写的程序速度快，但这样会导致执行速度更慢。  
  
## <a name="strong-typing"></a>强类型  
 指定为所有变量的数据类型被称为*强类型化*。 使用强类型化有几个优点︰  
  
-   它使您的变量的 IntelliSense 支持。 这样，您可以在代码中键入时看到它们的属性和其他成员。  
  
-   它可利用的编译器类型检查。 这将捕获在运行时由于如溢出错误而失败的语句。 不支持它们的对象，它还捕获对方法的调用。  
  
-   这会导致更快地执行代码。  
  
## <a name="most-efficient-data-types"></a>最高效的数据类型  
 对于永远不会包含秒的小数部分的变量，整数数据类型将比非整型更加有效。 在[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，`Integer`和`UInteger`是最有效的数值类型。  
  
 对于分数，`Double`是最有效的数据类型，因为当前平台上的处理器执行以双精度浮点运算。 但是，操作与`Double`与整数类型，如速度快`Integer`。  
  
## <a name="specifying-data-type"></a>指定数据类型  
 使用[Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)来声明某个特定类型的变量。 同时可以通过指定其访问级别[公共](../../../../visual-basic/language-reference/modifiers/public.md)，[受保护](../../../../visual-basic/language-reference/modifiers/protected.md)，[朋友](../../../../visual-basic/language-reference/modifiers/friend.md)，或[专用](../../../../visual-basic/language-reference/modifiers/private.md)关键字，如以下示例所示。  
  
```  
Private x As Double  
Protected s As String  
```  
  
## <a name="character-conversion"></a>字符转换  
 `AscW`和`ChrW`函数以 unicode 格式进行操作。 您应使用这些优先`Asc`和`Chr`，它必须在执行和跳出执行 Unicode 转换。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.Strings.Asc%2A></xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A></xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 <xref:Microsoft.VisualBasic.Strings.Chr%2A></xref:Microsoft.VisualBasic.Strings.Chr%2A>   
 <xref:Microsoft.VisualBasic.Strings.ChrW%2A></xref:Microsoft.VisualBasic.Strings.ChrW%2A>   
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [数值数据类型](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [使用 IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense)
