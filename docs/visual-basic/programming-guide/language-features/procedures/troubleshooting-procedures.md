---
title: "故障排除过程 (Visual Basic 中) |Microsoft 文档"
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
- troubleshooting Visual Basic, procedures
- procedures, troubleshooting
- Visual Basic code, procedures
- troubleshooting procedures
- procedures, about procedures
ms.assetid: 525721e8-2e02-4f75-b5d8-6b893462cf2b
caps.latest.revision: 17
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
ms.openlocfilehash: a5445d6da982e4eea5b1047505e4bee3380ed472
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-procedures-visual-basic"></a>过程疑难解答 (Visual Basic)
此页列出在使用过程时可能发生的一些常见问题。  
  
## <a name="returning-an-array-type-from-a-function-procedure"></a>从函数过程返回的数组类型  
 如果`Function`过程返回数组数据类型，则无法使用`Function`要将值存储在数组的元素名称。 如果尝试这样做，编译器会将其解释为对的调用`Function`。 下面的示例将生成编译器错误。  
  
 `Function allOnes(ByVal n As Integer) As Integer()`  
  
 `For i As Integer = 1 To n - 1`  
  
 `' The following statement generates a`   `COMPILER ERROR`  `.`  
  
 `allOnes(i) = 1`  
  
 `Next i`  
  
 `' The following statement generates a`   `COMPILER ERROR`  `.`  
  
 `Return allOnes()`  
  
 `End Function`  
  
 该语句`allOnes(i) = 1`生成编译器错误，因为它看起来在调用`allOnes`用错误的数据类型的参数 (单一实例`Integer`而不是`Integer`数组)。 该语句`Return allOnes()`生成编译器错误，因为它看起来在调用`allOnes`不带参数。  
  
 **正确的方法︰**能够修改将返回一个数组的元素，定义一个内部数组中，为本地变量。 下面的示例编译而不出错。  
  
 [!code-vb[VbVbcnProcedures #&66;](./codesnippet/VisualBasic/troubleshooting-procedures_1.vb)]  
  
## <a name="argument-not-being-modified-by-procedure-call"></a>未修改的参数由过程调用  
 如果您想要允许更改基础调用代码中的参数的编程元素的过程，必须通过引用传递。 但是，即使按值传递过程仍可访问的元素的引用类型参数。  
  
-   **基础变量**。 若要允许替换基础的变量元素本身的值的过程，该过程必须声明该参数[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)。 此外，调用代码必须不在括号内，则实参，因为这样将重写`ByRef`传递机制。  
  
-   **引用类型的元素**。 如果将参数声明[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)，该过程不能修改基础的变量元素本身。 但是，如果参数为引用类型，该过程可以修改它指向的该对象的成员，即使它不能替换变量的值一样。 例如，如果参数是一个数组变量，该过程不能将一个新数组分配给它，但它可以更改一个或多个元素。 更改的元素将反映在调用代码中的基础数组变量。  
  
 下面的示例定义两个过程，获得数组变量通过值和操作对其元素。 过程`increase`只需添加一个对每个元素。 过程`replace`将一个新数组分配给该参数`a()`，然后添加一个对每个元素。 但是，重新分配不影响调用代码中的基础数组变量因为`a()`声明`ByVal`。  
  
 [!code-vb[VbVbcnProcedures #&35;](./codesnippet/VisualBasic/troubleshooting-procedures_2.vb)]  
  
 [!code-vb[VbVbcnProcedures #&38;](./codesnippet/VisualBasic/troubleshooting-procedures_3.vb)]  
  
 以下示例将对调用`increase`和`replace`。  
  
 [!code-vb[VbVbcnProcedures #&37;](./codesnippet/VisualBasic/troubleshooting-procedures_4.vb)]  
  
 第一个`MsgBox`调用显示"之后 increase(n): 11、 21、 31、 41"。 因为`n`是引用类型，`increase`可以更改其中一个成员，即使它传递`ByVal`。  
  
 第二个`MsgBox`调用显示"之后 replace(n): 11、 21、 31、 41"。 因为`n`传递`ByVal`，`replace`不能修改该变量`n`通过向它分配一个新数组。 当`replace`创建新的数组实例`k`并将其分配给本地变量`a`，它将失去对引用`n`由调用代码传入的。 当它递增的成员`a`，只有本地数组`k`受到影响。  
  
 **正确的方法︰**能够修改基础的变量元素本身，通过引用传递。 下面的示例的声明中显示的更改`replace`允许它将替换为调用的代码中的另一个数组。  
  
 [!code-vb[VbVbcnProcedures #&64;](./codesnippet/VisualBasic/troubleshooting-procedures_5.vb)]  
  
## <a name="unable-to-define-an-overload"></a>无法定义重载方法  
 如果你想要定义一个过程的重载的版本，则必须使用相同的名称但不同的签名。 如果编译器无法区分具有相同签名的重载将声明，它会生成错误。  
  
 *签名*的过程由过程名称和参数列表。 每个重载必须具有与所有其他重载相同的名称，但必须不同于所有人中至少一个签名的其他组件。 有关详细信息，请参阅[过程重载](./procedure-overloading.md)。  
  
 以下各项，即使它们与参数列表中，不是过程签名的组件︰  
  
-   过程修饰符关键字，如`Public`， `Shared`，和`Static`  
  
-   参数名称  
  
-   参数修饰符关键字，如`ByRef`和`Optional`  
  
-   返回值 （转换运算符除外） 的数据类型  
  
 不能通过一个或多个上述各项只改变重载的过程。  
  
 **正确的方法︰**能够定义过程重载，您必须改变签名。 因为您必须使用相同的名称，您必须改变数量、 顺序或参数的数据类型。 在一般的过程中，您可以更改类型参数的数目。 在转换运算符 ([CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md))，可以指定不同的返回类型。  
  
### <a name="overload-resolution-with-optional-and-paramarray-arguments"></a>重载带有可选的分辨率和 ParamArray 参数  
 如果重载具有一个或多个过程[可选](../../../../visual-basic/language-reference/modifiers/optional.md)参数或[ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)参数，则必须避免复制任何*隐式重载*。 有关信息，请参阅[中重载过程注意事项](./considerations-in-overloading-procedures.md)。  
  
## <a name="calling-a-wrong-version-of-an-overloaded-procedure"></a>调用重载过程的不正确版本  
 如果过程具有多个重载的版本，你应该熟悉它们的参数列表并了解如何[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]之间重载解析调用。 否则，您可以调用非预期的重载。  
  
 当你已确定你想要调用的重载时，小心地将其遵守以下规则︰  
  
-   提供正确数量的参数，并以正确的顺序。  
  
-   理想情况下，您的参数应具有与对应的参数完全相同的数据类型。 在任何情况下，每个参数的数据类型必须扩大到其对应的参数。 这甚至对于一点[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)设置为`Off`。 如果某个重载需要从参数列表中，该重载的任何收缩转换是不能调用。  
  
-   如果您提供需要扩大的参数，使它们尽可能接近，到对应的参数数据类型的数据类型。 如果两个或多个重载接受您的参数数据类型，则编译器将解析对最少量的扩大转换为调用的重载的调用。  
  
 可以通过使用降低的数据类型不匹配的机率[CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)转换关键字准备参数时。  
  
### <a name="overload-resolution-failure"></a>重载解析失败  
 当调用重载的过程时，编译器会尝试消除所有但的重载之一。 如果成功，它可消除对该重载的调用。 如果它消除了所有重载，或者如果它不能减少为单个候选资格的重载，它将产生错误。  
  
 下面的示例阐释了重载决策过程。  
  
 [!code-vb[VbVbcnProcedures #&62;](./codesnippet/VisualBasic/troubleshooting-procedures_6.vb)]  
  
 [!code-vb[VbVbcnProcedures #&63;](./codesnippet/VisualBasic/troubleshooting-procedures_7.vb)]  
  
 在第一个调用中，编译器消除第一个重载，因为第一个参数的类型 (`Short`) 缩小到相应的参数的类型 (`Byte`)。 它然后能消除第三个重载，因为每个参数类型中的第二个重载 (`Short`和`Single`) 加宽到第三个重载中的相应类型 (`Integer`和`Single`)。 第二个重载需要扩大量较少，因此编译器将用它的调用。  
  
 在第二个调用中，编译器不能消除任何根据收缩重载。 因为它可以调用带参数类型的最少扩大的第二个重载，它会出于同样的原因如下所示的第一个调用，消除第三个重载。 但是，编译器无法解析的第一个和第二个重载之间。 每个已扩大为中其他的相应类型的一种已定义的参数类型 (`Byte`到`Short`，但`Single`到`Double`)。 因此，编译器会生成重载解析错误。  
  
 **正确的方法︰**若要能够调用重载的过程不二义性的情况下，使用[CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)以匹配为形参类型的参数数据类型。 下面的示例演示如何调用`z`强制解析到的第二个重载。  
  
 [!code-vb[VbVbcnProcedures #&65;](./codesnippet/VisualBasic/troubleshooting-procedures_8.vb)]  
  
### <a name="overload-resolution-with-optional-and-paramarray-arguments"></a>重载带有可选的分辨率和 ParamArray 参数  
 如果某个过程的两个重载具有相同的签名只是声明的最后一个参数[可选](../../../../visual-basic/language-reference/modifiers/optional.md)合一和[ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)中另一个，则编译器将解析对根据最接近的匹配该过程的调用。 有关详细信息，请参阅[重载解析](./overload-resolution.md)。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [Sub 过程](./sub-procedures.md)   
 [Function 过程](./function-procedures.md)   
 [属性过程](./property-procedures.md)   
 [运算符过程](./operator-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [过程重载](./procedure-overloading.md)   
 [重载过程注意事项](./considerations-in-overloading-procedures.md)   
 [重载决策](./overload-resolution.md)
