---
title: "重载过程 (Visual Basic 中) 注意事项 |Microsoft 文档"
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
- signatures, ParamArray arguments
- ParamArray keyword, parameter arrays
- ParamArray keyword, arguments and signatures
- function overloading, implicit overloads for ParamArray
- ParamArray keyword, signatures
- Visual Basic code, procedures
- arguments [Visual Basic], parameter arrays
- procedures, overloading
- parameters, lists
- function overloading, typeless programming
- typeless programming
- function overloading, restrictions
- arguments [Visual Basic], optional
- optional arguments, overloading
- signatures, procedure
- parameter lists
- parameter arrays, overloading arguments
- Visual Basic code, parameter lists
- procedure overloading, considerations
- Option Explicit statement
- restrictions, overloading procedures
- procedures, parameter lists
ms.assetid: a2001248-10d0-42c5-b0ce-eeedc987319f
caps.latest.revision: 26
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
ms.openlocfilehash: aa20cf367fba157f88afd861a4799540dcdecde1
ms.lasthandoff: 03/13/2017

---
# <a name="considerations-in-overloading-procedures-visual-basic"></a>重载过程注意事项 (Visual Basic)
重载过程，您必须使用不同*签名*对每个重载版本。 这通常意味着每个版本都必须指定不同的参数列表。 有关详细信息，请参阅"不同的签名"[过程重载](./procedure-overloading.md)。  
  
 您可以重载`Function`过程`Sub`的过程中，反之亦然，只要它们具有不同的签名和。 两个重载的不能区别仅在于其中一个具有一个返回值，而另一个不。  
  
 可重载属性相同的方式重载的过程，并采用相同的限制。 但是，不能重载的过程与属性，反之亦然。  
  
## <a name="alternatives-to-overloaded-versions"></a>重载版本的替代方法  
 特别是可选的参数存在或其数量是变量时，有时需要重载版本的替代方法。  
  
 请记住，可选参数不是支持所有语言和参数数组仅限于[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。 如果您正在编写一个过程，可能会以任何若干不同的语言编写的代码中调用，那么重载版本提供最大的灵活性。  
  
### <a name="overloads-and-optional-arguments"></a>重载和可选参数  
 当调用的代码 （可选） 可以提供，或者忽略一个或多个参数时，可以定义多个重载的版本，或使用可选参数。  
  
#### <a name="when-to-use-overloaded-versions"></a>何时使用重载的版本  
 您可以考虑在以下情况下定义一系列的重载版本︰  
  
-   在过程代码中的逻辑是明显不同，具体取决于是否，调用代码是否提供一个可选参数。  
  
-   过程代码不能可靠地测试是否调用代码提供一个可选参数。 这是这种情况，例如，如果没有可能的候选对于默认值调用的代码可能不会提供。  
  
#### <a name="when-to-use-optional-parameters"></a>何时使用可选参数  
 您可能更愿意在以下情况下的一个或多个可选参数︰  
  
-   唯一必需的操作时调用的代码不会提供一个可选参数是将参数设置为默认值。 在这种情况下，该过程代码可以降低复杂程度如果定义一个或多个单个版本`Optional`参数。  
  
 有关详细信息，请参阅[可选参数](./optional-parameters.md)。  
  
### <a name="overloads-and-paramarrays"></a>参数和重载  
 如果调用代码可以通过可变数量的参数，可以定义多个重载的版本，或者使用参数数组。  
  
#### <a name="when-to-use-overloaded-versions"></a>何时使用重载的版本  
 您可以考虑在以下情况下定义一系列的重载版本︰  
  
-   您知道，调用代码永远不会传递多个值一小部分给参数数组。  
  
-   在过程代码中的逻辑是明显不同，具体取决于调用代码传递的多少个值。  
  
-   调用代码可以通过不同的数据类型的值。  
  
#### <a name="when-to-use-a-parameter-array"></a>何时使用参数数组  
 您可能会更好的`ParamArray`参数在以下情况︰  
  
-   您不能预测多少个值调用代码可以传递给参数数组，它可能是大量。  
  
-   过程逻辑人士遍历所有通过调用代码，执行对每个值实质上是相同的操作的值。  
  
 有关详细信息，请参阅[参数数组](./parameter-arrays.md)。  
  
## <a name="implicit-overloads-for-optional-parameters"></a>可选参数的隐式重载  
 使用过程[可选](../../../../visual-basic/language-reference/modifiers/optional.md)参数等效于两个重载过程，一个带有可选参数，如果没有该软件的一个。 您不能具有参数列表对应于其中任何一种重载这样的过程。 下面的声明说明这一点。  
  
 [!code-vb[VbVbcnProcedures #&58; 页](./codesnippet/VisualBasic/considerations-in-overloading-procedures_1.vb)]  
  
 [!code-vb[VbVbcnProcedures #&60;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_2.vb)]  
  
 [!code-vb[VbVbcnProcedures #&61;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_3.vb)]  
  
 对于带多个可选参数的过程，没有隐式重载，到达由逻辑类似于前面的示例中的一组。  
  
## <a name="implicit-overloads-for-a-paramarray-parameter"></a>ParamArray 参数的隐式重载  
 编译器会考虑使用为过程[ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)参数具有无限数目的重载，不同于彼此中新增功能调用代码将传递给参数数组，如下所示︰  
  
-   当调用的代码不会提供的参数的一个重载`ParamArray`  
  
-   调用代码时提供的一维数组的一个重载`ParamArray`元素类型  
  
-   对于每个正整数时, 的重载调用的代码提供该数量的参数，每个`ParamArray`元素类型  
  
 下面的声明说明了这些隐式重载。  
  
 [!code-vb[VbVbcnProcedures #&68;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_4.vb)]  
  
 [!code-vb[VbVbcnProcedures #&70;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_5.vb)]  
  
 无法重载这种过程，将一维数组的参数数组的参数列表。 但是，您可以使用其他隐式重载的签名。 下面的声明说明这一点。  
  
 [!code-vb[VbVbcnProcedures #&71;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_6.vb)]  
  
## <a name="typeless-programming-as-an-alternative-to-overloading"></a>作为重载的替代方法的无类型编程  
 如果您想要使调用代码将不同的数据类型传递给一个参数，另一种方法是无类型编程。 您可以设置类型检查切换到`Off`与[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)或[/optionstrict](../../../../visual-basic/reference/command-line-compiler/optionstrict.md)编译器选项。 然后您不需要声明参数的数据类型。 但是，此方法具有以下缺点相比重载︰  
  
-   无类型编程生成效率较低的执行代码。  
  
-   该过程必须测试预期将传递每个数据类型。  
  
-   如果调用代码传递过程不支持的数据类型，编译器不能发出错误。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [故障排除过程](./troubleshooting-procedures.md)   
 [如何︰ 定义一个过程的多个版本](./how-to-define-multiple-versions-of-a-procedure.md)   
 [如何︰ 调用重载的过程](./how-to-call-an-overloaded-procedure.md)   
 [如何︰ 重载带有可选参数的过程](./how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [如何︰ 重载参数数量不确定的过程](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [重载决策](./overload-resolution.md)   
 [重载](../../../../visual-basic/language-reference/modifiers/overloads.md)
