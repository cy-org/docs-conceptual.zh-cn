---
title: "使用字符串名称 (Visual Basic 中) 调用属性或方法 |Microsoft 文档"
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
- passing operators
- strings [Visual Basic], passing new operators as
- objects [Visual Basic], setting properties
- setting properties, object properties at run time
- method calls, strings
- methods [Visual Basic], calling with string names
- calling methods, string names
- properties [Visual Basic], setting at run time
- CallByName function
ms.assetid: 79a7b8b4-b8c7-4ad8-aca8-12a9a2b32f03
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
ms.openlocfilehash: 87af2816ba42e2901c53bec5e9c19f34c676ed5c
ms.lasthandoff: 03/13/2017

---
# <a name="calling-a-property-or-method-using-a-string-name-visual-basic"></a>使用字符串名调用属性或方法 (Visual Basic)
在大多数情况下，可以在设计时发现的属性和对象的方法，并编写代码来处理它们。 但是，在某些情况下您可能事先不知道有关对象的属性和方法，或者可能只是需要灵活性，使最终用户可以指定属性或在运行时执行的方法。  
  
## <a name="callbyname-function"></a>CallByName 函数  
 例如，考虑通过将运算符传递给 COM 组件的用户输入的表达式的计算结果的客户端应用程序。 假设要不断地向需要新的运算符的组件中添加新函数。 当您使用标准对象访问技术时，您必须重新编译并重新分发客户端应用程序，可以使用新的运算符之前。 若要避免此问题，可以使用`CallByName`函数运算符来传递新形式的字符串，而无需更改应用程序。  
  
 `CallByName`函数允许您使用一个字符串，在运行时指定的属性或方法。 签名`CallByName`函数如下所示︰  
  
 *Result* = `CallByName`(*Object*, *ProcedureName*, *CallType*, *Arguments*())  
  
 第一个参数，*对象*，采用您想要对其执行操作的对象的名称。 *过程名*参数采用一个字符串，包含要调用的方法或属性的过程的名称。 *CallType*参数采用一个常量，它表示要调用过程的类型︰ 一种方法 (`Microsoft.VisualBasic.CallType.Method`)，读取的属性 (`Microsoft.VisualBasic.CallType.Get`)，或一个设置的属性 (`Microsoft.VisualBasic.CallType.Set`)。 *参数*参数，它是可选的采用的类型数组`Object`，其中包含任何参数的过程。  
  
 您可以使用`CallByName`与您当前的解决方案，但它的类是最常用于访问 COM 对象或对象从[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]程序集。  
  
 假设您添加对包含一个名为类的程序集的引用`MathClass`，它具有一个名为的新函数`SquareRoot`，如下面的代码中所示︰  
  
 [!code-vb[VbVbalrOOP #&53;](../../../../visual-basic/misc/codesnippet/VisualBasic/calling-a-property-or-method-using-a-string-name_1.vb)]  
  
 您的应用程序可以使用文本框控件来控制将要调用的方法和它的参数。 例如，如果`TextBox1`包含要计算的表达式和`TextBox2`是用于输入的函数名称，可以使用下面的代码来调用`SquareRoot`函数中的表达式在`TextBox1`:  
  
 [!code-vb[VbVbalrOOP #&54;](../../../../visual-basic/misc/codesnippet/VisualBasic/calling-a-property-or-method-using-a-string-name_2.vb)]  
  
 如果在输入"64"`TextBox1`中的"SquareRoot" `TextBox2`，然后调用`CallMath`过程、 采用的数字的平方根`TextBox1`计算。 该示例中的代码时，将调用`SquareRoot`函数 （将一个字符串，包含要作为一个必需的参数计算的表达式），并返回以"8" `TextBox1` （64 的平方根）。 当然，如果用户输入中的无效字符串`TextBox2`，如果该字符串包含而不是一种方法，属性的名称，或者如果该方法有一个额外的必需的参数，发生在运行时错误。 您必须添加可靠的错误处理代码，当您使用`CallByName`以应对预期的这些数据或任何其他错误。  
  
> [!NOTE]
>  虽然`CallByName`函数可能会很有用，在某些情况下，您必须权衡的性能影响针对其有用性 — 使用`CallByName`以调用过程会稍慢些比后期绑定调用。 如果所调用的函数被重复调用，例如在循环中，如`CallByName`会产生严重影响性能。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.Interaction.CallByName%2A></xref:Microsoft.VisualBasic.Interaction.CallByName%2A>   
 [确定对象类型](../../../../visual-basic/programming-guide/language-features/early-late-binding/determining-object-type.md)
