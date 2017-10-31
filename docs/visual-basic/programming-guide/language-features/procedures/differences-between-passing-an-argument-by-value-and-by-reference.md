---
title: "通过值和通过引用 (Visual Basic 中) 传递参数之间的差异 |Microsoft 文档"
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
- procedures, passing arguments
- ByVal keyword, passing arguments by value
- arguments [Visual Basic], passing by value or by reference
ms.assetid: 5f5c38fe-3e2d-494c-8fff-f4025b55ec93
caps.latest.revision: 14
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
ms.openlocfilehash: 93c515dd8524cde85555a27879baee00185f78e3
ms.lasthandoff: 03/13/2017

---
# <a name="differences-between-passing-an-argument-by-value-and-by-reference-visual-basic"></a>通过值传递自变量和通过引用传递自变量之间的差异 (Visual Basic)
当将一个或多个参数传递给过程中时，每个参数对应一个基础编程元素调用的代码中。 您可以传递此基础元素的值，或者对它的引用。 这称为*传递机制*。  
  
## <a name="passing-by-value"></a>按值传递  
 传递了参数*按值*通过指定[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)在过程定义中的相应参数的关键字。 当您使用此传递机制，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将基础编程元素的值复制到该过程中的局部变量。 过程代码中调用代码没有的任何访问权限的基础元素。  
  
## <a name="passing-by-reference"></a>通过引用传递  
 传递了参数*通过引用*通过指定[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)在过程定义中的相应参数的关键字。 当您使用此传递机制，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使过程的基础的编程元素的直接引用中调用代码。  
  
## <a name="passing-mechanism-and-element-type"></a>传递机制和元素类型  
 选择传递机制不是相同的基本元素类型的分类。 按值或按引用传递是指什么[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供给该过程代码。 值类型或引用类型是指在内存中存储的编程元素的方式。  
  
 但是，传递机制和元素类型是相互关联。 引用类型的值是一个指向内存中其他位置的数据。 也就是说，当通过值传递引用类型时，过程代码中有一个指向基础元素的数据，即使它不能访问基础元素本身也是如此。 例如，如果该元素是一个数组变量，过程代码不具有访问变量本身，但它可以访问数组成员。  
  
## <a name="ability-to-modify"></a>若要修改的能力  
 当作为参数传递不可更改元素时，过程可以永远不会修改它在调用代码中，不论它的传入`ByVal`或`ByRef`。  
  
 对于可修改的元素下, 表总结了元素类型和传递机制之间的交互。  
  
|元素类型|传递`ByVal`|传递`ByRef`|  
|------------------|--------------------|--------------------|  
|值类型 （包含只有一个值）|该过程不能更改该变量或任何成员。|该过程可以更改变量和其成员。|  
|引用类型 （包含指向类或结构的实例的指针）|该过程不能更改变量，但可以更改它所指向的实例的成员。|该过程可以更改变量和它所指向的实例的成员。|  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [如何︰ 将参数传递给过程](./how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](./passing-arguments-by-value-and-by-reference.md)   
 [可修改和不可修改参数之间的差异](./differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [如何︰ 更改过程参数的值](./how-to-change-the-value-of-a-procedure-argument.md)   
 [如何︰ 防止过程参数的值更改](./how-to-protect-a-procedure-argument-against-value-changes.md)   
 [如何︰ 强制通过值传递参数](./how-to-force-an-argument-to-be-passed-by-value.md)   
 [按位置和按名称传递参数](./passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
