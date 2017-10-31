---
title: "CType 函数 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.CType"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "表达式转换结果"
  - "显式数据类型转换"
  - "CType 函数"
  - "转换，表达式"
ms.assetid: dd4b29e7-6fa1-428c-877e-69955420bb72
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# CType 函数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

返回表达式显式转换为指定的数据类型、对象、结构、类或接口的结果。  
  
## 语法  
  
```  
CType(expression, typename)  
```  
  
## 部件  
 `expression`  
 任何有效的表达式。  如果 `expression` 的值超出 `typename` 允许的范围，Visual Basic 将引发异常。  
  
 `typename`  
 任何在 `Dim` 语句的 `As` 子句内合法的表达式，即任何数据类型、对象、结构、类或接口的名称。  
  
## 备注  
  
> [!TIP]
>  您也可以使用以下函数来执行类型转换：  
>   
>  -   键入用于对特定数据类型进行转换的 `CByte`、`CDbl` 和 `CInt` 等转换函数。  有关详细信息，请参阅 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)。  
> -   [DirectCast 运算符](../../../visual-basic/language-reference/operators/directcast-operator.md) 或 [TryCast 运算符](../../../visual-basic/language-reference/operators/trycast-operator.md)。  这些运算符要求一个类型必须继承自或实现另一个类型。  当转换至和从 `Object` 数据类型转换时，他们可以提供一些比 `CType` 更佳的性能。  
  
 `CType` 采用内联方式编译，即转换代码是计算表达式的代码的一部分。  在某些情况下，由于未调用过程来执行转换，因此代码运行较快。  
  
 如果没有定义从 `expression` 到 `typename` 的转换，（例如从 `Integer` 转换到 `Date`），Visual Basic 将显示一条编译时错误消息。  
  
 如果在运行时转换失败，将会引发相应的异常。  如果收缩转换失败，最常见的结果是 <xref:System.OverflowException>。  如果未定义转换，将会发生 <xref:System.InvalidCastException>。  例如，如果 `expression` 的类型为 `Object`，并且其运行时类型没有转换为 `typename`，则可能会发生这种情况。  
  
 如果 `expression` 或 `typename` 的数据类型为已经定义的类或结构，则可以在该类或结构中将 `CType` 定义为转换运算符。  这将使 `CType` 用作重载运算符。  如果这样做，则可以控制转换在类或结构之间进行的转换的行为，包括可能引发的异常。  
  
## 重载  
 `CType` 运算符也可以在代码之外定义的类或结构中重载。  如果您的代码需要在这样的类或结构之间进行转换，请确定您了解其 `CType` 运算符的行为。  有关详细信息，请参阅 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 转换动态对象  
 动态对象的类型转换由使用 <xref:System.Dynamic.DynamicObject.TryConvert%2A> 或 <xref:System.Dynamic.DynamicMetaObject.BindConvert%2A> 方法的用户定义的动态转换执行。  如果您使用动态对象，请使用 <xref:Microsoft.VisualBasic.Conversion.CTypeDynamic%2A> 方法转换动态对象。  
  
## 示例  
 下面的示例使用 `CType` 函数将表达式转换为指定的 `Single` 数据类型。  
  
 [!code-vb[VbVbalrFunctions#24](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/ctype-function_1.vb)]  
  
 有关其他示例，请参见[隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)。  
  
## 请参阅  
 <xref:System.OverflowException>   
 <xref:System.InvalidCastException>   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换函数](../../../visual-basic/language-reference/functions/conversion-functions.md)   
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [如何：定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [.NET Framework 中的类型转换](../Topic/Type%20Conversion%20in%20the%20.NET%20Framework.md)