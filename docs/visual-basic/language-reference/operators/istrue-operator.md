---
title: "IsTrue 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.istrue"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "IsTrue 运算符"
  - "OrElse 运算符 [Visual Basic]"
ms.assetid: b6cec0f2-61b1-4331-a7f0-4d07ee3179d6
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# IsTrue 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

确定一个表达式是否是 `True`。  
  
 不能在代码中显式调用 `IsTrue`，但 Visual Basic 编译器可以用它从 `OrElse` 子句生成代码。  如果您定义一个类或结构，然后在 `OrElse` 子句中使用这种类型的变量，则必须在该类或结构上定义 `IsTrue`。  
  
 编译器将 `IsTrue` 和 `IsFalse` 运算符当作匹配对。  这意味着如果您定义其中一个运算符，则还必须定义另外一个。  
  
## IsTrue 的编译器运用  
 如果定义了一个类或结构，则可以在 `For`、`If`、`Else` `If` 或 `While` 语句或者 `When` 子句中使用此类型的变量。  如果执行此操作，编译器需要使用一个将此类型转换为 `Boolean` 值的运算符，以便可以测试条件。  编译器将按以下顺序搜索合适的运算符：  
  
1.  类或结构中可扩大为 `Boolean` 的扩大转换运算符。  
  
2.  类或结构中可扩大为 `Boolean?` 的扩大转换运算符。  
  
3.  类或结构中的 `IsTrue` 运算符。  
  
4.  不涉及从 `Boolean` 到 `Boolean?` 的转换的 `Boolean?` 收缩转换。  
  
5.  类或结构中可收缩为 `Boolean` 的收缩转换运算符。  
  
 如果尚未将任何转换定义到 `Boolean` 或 `IsTrue` 运算符，编译器将发出错误信号。  
  
> [!NOTE]
>  `IsTrue` 运算符可以被重载，这意味着当该运算符的操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的代码示例定义一个结构的大致形式，此结构包含 `IsFalse` 和 `IsTrue` 运算符的定义。  
  
 [!code-vb[VbVbalrOperators#28](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/istrue-operator_1.vb)]  
  
## 请参阅  
 [IsFalse 运算符](../../../visual-basic/language-reference/operators/isfalse-operator.md)   
 [如何：定义运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [OrElse 运算符](../../../visual-basic/language-reference/operators/orelse-operator.md)