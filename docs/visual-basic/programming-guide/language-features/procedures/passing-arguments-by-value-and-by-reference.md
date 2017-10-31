---
title: "传递参数通过值和通过引用 (Visual Basic 中) |Microsoft 文档"
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
- ByRef keyword, passing arguments by reference
- Visual Basic code, procedures
- passing arguments, by value or by reference
- ByVal keyword, passing arguments by value
- arguments [Visual Basic], passing by value or by reference
- argument passing, by value or by reference
ms.assetid: fd8a9de6-7178-44d5-a9bf-458d4ad907c2
caps.latest.revision: 23
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
ms.openlocfilehash: 56d1ceba14020ca7f3dc750c2318efd3e9586af0
ms.lasthandoff: 03/13/2017

---
# <a name="passing-arguments-by-value-and-by-reference-visual-basic"></a>通过值和通过引用传递自变量 (Visual Basic)
在[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，可以将参数传递给过程*按值*或*通过引用*。 这称为*传递机制*，并确定该过程是否可以修改调用代码中的实参的编程元素。 过程声明确定每个参数的传递机制，通过指定[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)或[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)关键字。  
  
## <a name="distinctions"></a>区别  
 如果将参数传递给过程，应注意的几点彼此交互的差异︰  
  
-   基础的编程元素是可修改还是不可更改  
  
-   参数本身是可修改或不可更改  
  
-   参数按值或按引用传递  
  
-   参数数据类型是否是值类型或引用类型  
  
 有关详细信息，请参阅[差异之间可修改和不可修改参数](./differences-between-modifiable-and-nonmodifiable-arguments.md)和[差异之间传递的参数值和通过引用来](./differences-between-passing-an-argument-by-value-and-by-reference.md)。  
  
## <a name="choice-of-passing-mechanism"></a>选择传递机制  
 您应选择小心地为每个参数传递机制。  
  
-   **保护**。 在两个传递机制之间进行选择，最重要的条件是公开的调用要更改的变量。 传递参数的优点`ByRef`是该过程可以返回给调用代码通过该参数的值。 传递参数的优点`ByVal`是它可防止一个变量的过程更改。  
  
-   **性能**。 尽管传递机制可能会影响您的性能，不同之处是代码的通常并不显著。 一个例外是值类型传递`ByVal`。 在这种情况下，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]复制参数的整个数据内容。 因此，较大的值类型，如一个结构，它可以更高效，以将其传递`ByRef`。  
  
     对于引用类型，只对数据的指针是复制 （4 个字节在 32 位平台上，在 64 位平台上的 8 个字节）。 因此，可以将类型的参数传递`String`或`Object`的值，而不损害性能的前提下。  
  
## <a name="determination-of-the-passing-mechanism"></a>确定的传递机制  
 过程声明中指定的每个参数的传递机制。 调用代码不能重写`ByVal`机制。  
  
 如果参数用声明`ByRef`，调用代码可以强制机制来`ByVal`通过括在圆括号来调用的参数名称。 有关详细信息，请参阅[如何︰ 强制通过值传递到参数](./how-to-force-an-argument-to-be-passed-by-value.md)。  
  
 中的默认设置[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]是按值传递参数。  
  
## <a name="when-to-pass-an-argument-by-value"></a>何时通过值传递参数  
  
-   如果调用参数的基础的代码元素是不可修改的元素，声明对应的形参[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)。 无代码可以更改不可更改元素的值。  
  
-   如果基础元素是可修改的但不是希望将无法更改其值的过程，将参数声明`ByVal`。 只有调用代码可以更改通过值传递的可修改元素的值。  
  
## <a name="when-to-pass-an-argument-by-reference"></a>当通过引用传递参数  
  
-   如果该过程具有确实需要更改的基础元素调用的代码中，声明对应的形参[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)。  
  
-   如果代码正确执行依赖于更改中调用代码的基础元素的过程，将参数声明`ByRef`。 如果将其传递的数值，或者调用代码重写`ByRef`传递机制，通过将实参括在括号内，则过程调用可能会产生意外的结果。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 以下示例说明何时通过值传递参数以及何时通过引用传递。 过程`Calculate`同时具有`ByVal`和`ByRef`参数。 给定利率， `rate`，和资金，总和`debt`，该过程的任务是来计算新值的`debt`，它是对应用的结果利率的原始值`debt`。 因为`debt`是`ByRef`参数，对应于调用代码中的参数的值中反映新的总`debt`。 参数`rate`是`ByVal`参数因为`Calculate`不应更改其值。  
  
### <a name="code"></a>代码  
 [!code-vb[VbVbcnProcedures #&74;](./codesnippet/VisualBasic/passing-arguments-by-value-and-by-reference_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [如何︰ 将参数传递给过程](./how-to-pass-arguments-to-a-procedure.md)   
 [如何︰ 更改过程参数的值](./how-to-change-the-value-of-a-procedure-argument.md)   
 [如何︰ 防止过程参数的值更改](./how-to-protect-a-procedure-argument-against-value-changes.md)   
 [如何︰ 强制通过值传递参数](./how-to-force-an-argument-to-be-passed-by-value.md)   
 [按位置和按名称传递参数](./passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
