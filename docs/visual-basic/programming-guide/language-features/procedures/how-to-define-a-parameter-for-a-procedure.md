---
title: "如何︰ 为过程 (Visual Basic 中) 中定义参数 |Microsoft 文档"
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
- procedure parameters, defining data types for
- procedures, parameters
- procedures, defining
- Visual Basic code, procedures
- procedure parameters, defining
ms.assetid: 7962808d-407e-4e84-984e-43e9857c53c9
caps.latest.revision: 15
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
ms.openlocfilehash: 9fb9ad244499039c1768ff97f071168e0a0842e4
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-define-a-parameter-for-a-procedure-visual-basic"></a>如何：为过程定义参数 (Visual Basic)
一个*参数*允许调用的代码将值传递给该过程，在它调用时。 声明一个过程的每个参数相同的方式声明变量，指定其名称和数据类型。 您还指定传递机制，以及该参数是否可选。  
  
 有关详细信息，请参阅[过程参数和变量](./procedure-parameters-and-arguments.md)。  
  
### <a name="to-define-a-procedure-parameter"></a>若要定义过程参数  
  
1.  在过程声明中，将添加到过程的参数列表，用逗号将它与其他参数的参数名称。  
  
2.  确定参数的数据类型。  
  
3.  请按照参数名称后的加`As`子句来指定数据类型。  
  
4.  确定所需的参数的传递机制。 通常情况下参数按值传递，除非您想要能够更改它的值调用的代码中的过程。  
  
5.  参数名称前面加上[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)或[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)指定传递机制。 有关详细信息，请参阅[差异之间传递的参数值和通过引用来](./differences-between-passing-an-argument-by-value-and-by-reference.md)。  
  
6.  如果该参数是可选的在前面的传递机制与[可选](../../../../visual-basic/language-reference/modifiers/optional.md)，然后按照参数的数据类型以等号 (`=`) 和默认值。  
  
     下面的示例定义的轮廓`Sub`带有三个参数的过程。 前两个要求，并且第三个是可选的。 参数声明由逗号分隔的参数列表中。  
  
     [!code-vb[VbVbcnProcedures 第&33;](./codesnippet/VisualBasic/how-to-define-a-parameter-for-a-procedure_1.vb)]  
  
     第一个参数接受`customer`对象，并`updateCustomer`可以直接更新该变量传递给`c`因为则参数进行传递[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)。 该过程不能更改最后两个参数的值，因为它们传递[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)。  
  
     如果调用代码不会提供的值`level`参数，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将其设置为默认值为 0。  
  
     如果类型检查开关 ([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) 是`Off`、`As`子句是可选的当您定义参数。 但是，如果任何一个参数使用`As`子句中，所有人必须使用它。 如果类型检查开关是`On`、`As`子句是必需的每个参数定义。  
  
     指定所有编程元素的数据类型被称为*强类型化*。 当您将设置`Option Strict On`，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]强制使用强类型化。 这是强烈建议，原因如下︰  
  
    -   它使您的变量和参数的 IntelliSense 支持。 这样，您可以在您的代码中键入时看到它们的属性和其他成员。  
  
    -   它允许编译器执行类型检查。 这可帮助捕获在运行时由于如溢出错误而失败的语句。 不支持它们的对象，它还捕获对方法的调用。  
  
    -   这会导致更快地执行代码。 一种的原因是，如果您未指定的编程元素的数据类型[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将其分配`Object`类型。 已编译的代码可能需要将之间来回转换`Object`和其他数据类型，这会降低性能。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [Sub 过程](./sub-procedures.md)   
 [Function 过程](./function-procedures.md)   
 [如何︰ 将参数传递给过程](./how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](./passing-arguments-by-value-and-by-reference.md)   
 [递归过程](./recursive-procedures.md)   
 [过程重载](./procedure-overloading.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [面向对象的编程](http://msdn.microsoft.com/library/1cf6e655-3f30-45f1-9a5d-4a88ca24a1c2)
