---
title: "IsFalse 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.isfalse"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "AndAlso 运算符"
  - "IsFalse 运算符"
ms.assetid: 37fc9dbf-e5cc-4570-b93f-7213447974df
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# IsFalse 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

确定一个表达式是否是 `False`。  
  
 不能在代码中显式调用 `IsFalse`，但 Visual Basic 编译器可以用它从 `AndAlso` 子句生成代码。  如果您定义一个类或结构，然后在 `AndAlso` 子句中使用这种类型的变量，则必须在该类或结构上定义 `IsFalse`。  
  
 编译器将 `IsFalse` 和 `IsTrue` 运算符当作匹配对。  这意味着如果您定义其中一个运算符，则还必须定义另外一个。  
  
> [!NOTE]
>  `IsFalse` 运算符可以被“重载”，这意味着当该运算符的操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的代码示例定义一个结构的大致形式，此结构包含 `IsFalse` 和 `IsTrue` 运算符的定义。  
  
 [!code-vb[VbVbalrOperators#28](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/isfalse-operator_1.vb)]  
  
## 请参阅  
 [IsTrue 运算符](../../../visual-basic/language-reference/operators/istrue-operator.md)   
 [如何：定义运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [AndAlso 运算符](../../../visual-basic/language-reference/operators/andalso-operator.md)