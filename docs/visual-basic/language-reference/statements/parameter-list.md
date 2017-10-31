---
title: "参数列表 (Visual Basic 中) |Microsoft 文档"
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
- Visual Basic code, procedures
- parameters, Visual Basic
- parameters, lists
- parameter lists
- Visual Basic code, parameter lists
- arguments [Visual Basic], Visual Basic
- procedures, parameter lists
ms.assetid: 5d737319-0c34-4df9-a23d-188fc840becd
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
ms.openlocfilehash: abadaa8e035bfa4c92acc30ab633d6a7e958676c
ms.lasthandoff: 03/13/2017

---
# <a name="parameter-list-visual-basic"></a>参数列表 (Visual Basic)
指定过程需要被调用时的参数。 由逗号分隔多个参数。 下面是一个参数的语法。  
  
## <a name="syntax"></a>语法  
  
```  
[ <attributelist> ] [ Optional ] [{ ByVal | ByRef }] [ ParamArray ]   
parametername[( )] [ As parametertype ] [ = defaultvalue ]  
```  
  
## <a name="parts"></a>部件  
 `attributelist`  
 可选。 将应用到此参数的属性列表。 必须将括[属性列表](../../../visual-basic/language-reference/statements/attribute-list.md)在尖括号 ("`<`"和"`>`")。  
  
 `Optional`  
 可选。 指定此参数不需要调用该过程时。  
  
 `ByVal`  
 可选。 指定该过程不能替换或重新分配下调用的代码中的对应参数的变量元素。  
  
 `ByRef`  
 可选。 指定该过程可以用相同的方式与调用代码本身可以修改调用代码中的基础变量元素。  
  
 `ParamArray`  
 可选。 指定的参数列表中的最后一个参数是一个指定的数据类型的元素的可选数组。 这样将任意数量的参数传递给过程的调用代码。  
  
 `parametername`  
 必需。 表示参数的本地变量的名称。  
  
 `parametertype`  
 如果使用`Option Strict`是`On`。 表示参数的本地变量的数据类型。  
  
 `defaultvalue`  
 所需的`Optional`参数。 任何常量或常量表达式的计算结果为该参数的数据类型。 如果类型为`Object`，或类、 接口、 数组或结构，默认值只能是`Nothing`。  
  
## <a name="remarks"></a>备注  
 参数是用括号括起来，并且用逗号隔开。 可以使用任何数据类型声明参数。 如果未指定`parametertype`，它将默认为`Object`。  
  
 当调用的代码调用该过程时，它将传递*参数*向每个所需的参数。 有关详细信息，请参阅[差异之间形参和实参](../../../visual-basic/programming-guide/language-features/procedures/differences-between-parameters-and-arguments.md)。  
  
 调用代码将传递给每个参数的参数是指向中调用代码的基础元素的指针。 如果此元素为*不可变元素*（常量、 文字、 枚举或表达式），它是不可能将其更改任何代码。 如果它是*变量*元素 （声明的变量、 字段、 属性、 数组元素或结构元素），调用代码可以对其进行更改。 有关详细信息，请参阅[差异之间可修改和不可修改参数](../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)。  
  
 如果传递的变量元素`ByRef`，该过程它也可以进行更改。 有关详细信息，请参阅[差异之间传递的参数值和通过引用来](../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)。  
  
## <a name="rules"></a>规则  
  
-   **括号。** 如果指定的参数列表，则必须将其括在括号中。 如果没有任何参数，您仍然可以使用括号内包含一个空列表。 这将通过清晰化元素一个过程提高代码的可读性。  
  
-   **可选参数。** 如果您使用`Optional`参数修饰符，列表中的所有后续参数也必须为可选和使用声明`Optional`修饰符。  
  
     每个可选参数声明必须提供`defaultvalue`子句。  
  
     有关详细信息，请参阅[可选参数](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)。  
  
-   **参数数组。** 必须指定`ByVal`为`ParamArray`参数。  
  
     您不能同时使用`Optional`和`ParamArray`在相同的参数列表中。  
  
     有关详细信息，请参阅[参数数组](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)。  
  
-   **传递机制。** 每个参数的默认机制是`ByVal`，这意味着该过程不能更改基础变量元素。 但是，如果该元素是引用类型，该过程可以修改内容或成员的基础对象，即使它不能替换或重新分配对象本身。  
  
-   **参数名称。** 如果参数的数据类型是一个数组，请按照`parametername`紧跟括号。 参数名称的详细信息，请参阅[声明元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示`Function`定义两个参数的过程。  
  
 [!code-vb[VbVbalrStatements #&2;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/parameter-list_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.DllImportAttribute></xref:System.Runtime.InteropServices.DllImportAttribute>   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [属性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)   
 [如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
