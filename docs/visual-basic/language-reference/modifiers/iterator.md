---
title: "迭代器 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Iterator"
helpviewer_keywords: 
  - "Iterator 关键字 [Visual Basic]"
ms.assetid: 69cb0b04-ac87-49d0-bcfe-810c0d60daff
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 迭代器 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定函数或 `Get` 访问器是迭代器。  
  
## 备注  
 *迭代器* 对集合的自定义迭代。  迭代器使用 [yield](../../../visual-basic/language-reference/statements/yield-statement.md) 语句返回集合中的每个元素一个节点。  当 `Yield` 语句时，代码的当前位置保留。  执行从该位置下次重新启动迭代器函数调用。  
  
 迭代器可以实现为函数或作为属性定义的 `Get` 访问器。  `Iterator` 修饰符出现在迭代器函数或 `Get` 访问器的说明。  
  
 使用 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)，请调用从客户端代码中的迭代器。  
  
 迭代器函数或 `Get` 访问器的返回类型可以是 <xref:System.Collections.IEnumerable>、 <xref:System.Collections.Generic.IEnumerable%601>、 <xref:System.Collections.IEnumerator>或 <xref:System.Collections.Generic.IEnumerator%601>。  
  
 迭代器不能有任何 `ByRef` 参数。  
  
 迭代器在事件、实例构造函数、静态构造函数或静态析构函数不能出现。  
  
 迭代器可以是匿名函数。  有关更多信息，请参见 [迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 有关迭代器的更多信息，请参见[迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 用法  
 `Iterator` 修饰符可用于下面的上下文中：  
  
-   [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
-   [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## 示例  
 下面的示例演示一个迭代器函数。  迭代器函数具有是在 [for…next](../../../visual-basic/language-reference/statements/for-next-statement.md) 循环内的一个 `Yield` 语句。  [对于每个](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 语句体的每个迭代在 `Main` 的创建调用 `Power` 迭代器函数。  每个调用迭代器函数提升到 `Yield` 语句的下执行，在 `For…Next` 循环的下一次迭代时发生。  
  
 [!code-vb[VbVbalrStatements#98](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/iterator_1.vb)]  
  
## 示例  
 下面的示例演示是迭代器的 `Get` 访问器。  `Iterator` 修饰符在属性声明。  
  
 [!code-vb[VbVbalrStatements#99](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/iterator_2.vb)]  
  
 有关其他示例，请参见[迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 请参阅  
 <xref:System.Runtime.CompilerServices.IteratorStateMachineAttribute>   
 [迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)   
 [Yield 语句](../../../visual-basic/language-reference/statements/yield-statement.md)