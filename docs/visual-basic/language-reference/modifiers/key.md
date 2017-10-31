---
title: "Key (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AnonymousKey"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "匿名类型 [Visual Basic], 键"
  - "Key [Visual Basic]"
  - "Key 关键字 [Visual Basic]"
ms.assetid: 7697a928-7d14-4430-a72a-c9e96e8d6c11
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Key (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`Key` 关键字使您可以为匿名类型的属性指定行为。  可以将为键属性仅的属性参与测试在匿名类型实例之间的哈希代码值是否相等或计算。  不能更改键属性的值。  
  
 可以将匿名类型的属性为键属性通过将在其声明前面的关键字 `Key` 在初始化列表。  在下面的示例中， `Airline` 和 `FlightNo` 为键属性，但是， `Gate` 不是。  
  
 [!code-vb[VbVbalrAnonymousTypes#26](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_1.vb)]  
  
 当一个新的匿名类型之后，它将直接从 <xref:System.Object>继承。  编译器将重写三个继承的成员: <xref:System.Object.Equals%2A>、 <xref:System.Object.GetHashCode%2A>和 <xref:System.Object.ToString%2A>。  为 <xref:System.Object.Equals%2A> 和 <xref:System.Object.GetHashCode%2A> 生成的重写代码根据键属性。  如果类型的键属性， <xref:System.Object.GetHashCode%2A> 和 <xref:System.Object.Equals%2A> 未被重写。  
  
## 相等  
 两个匿名类型实例相等; 如果它们属于同一类型的实例，并且，如果它们的主要属性的值相等。  在下面的示例中， `flight2` 与上一示例中的 `flight1` 相等，因为它们是相同匿名类型的实例，并且具有其主要属性匹配的值。  但是， `flight3` 与 `flight1` ，因为它有关键属性的值不同， `FlightNo`不相等。  ，因为它们指定不同的属性作为键属性，实例 `flight4` 不是类型和 `flight1` 相同。  
  
 [!code-vb[VbVbalrAnonymousTypes#27](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_2.vb)]  
  
 如果两个实例声明仅非键属性，按相同的名称、类型、序列和值，两个实例不相等。  没有关键属性的实例与自身仅相等。  
  
 有关两个匿名类型实例是相同匿名类型的实例的条件的更多信息，请参见 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
## 哈希代码计算  
 与 <xref:System.Object.Equals%2A>，在匿名类型的 <xref:System.Object.GetHashCode%2A> 定义的哈希函数基于类型的主要属性。  下面的示例演示主要属性和哈希代码值之间的交互。  
  
 具有任何项属性的相同值具有相同的哈希代码值匿名类型的实例，因此，即使非键属性没有匹配的值。  下列语句返回 `True`。  
  
 [!code-vb[VbVbalrAnonymousTypes#37](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_3.vb)]  
  
 具有一个或多个键属性的不同值具有不同匿名类型的实例的哈希代码值。  下列语句返回 `False`。  
  
 [!code-vb[VbVbalrAnonymousTypes#38](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_4.vb)]  
  
 指定不同的属性匿名类型的实例，因为键属性不属于同一类型的实例。  ，即使所有特性的名称和值相同，它们具有不同的哈希代码值。  下列语句返回 `False`。  
  
 [!code-vb[VbVbalrAnonymousTypes#39](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_5.vb)]  
  
## 只读值  
 不能更改键属性的值。  例如，在前面的示例中的 `flight1` ， `Airline` 和 `FlightNo` 字段是只读的，但是，可以更改 `Gate` 。  
  
 [!code-vb[VbVbalrAnonymousTypes#28](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_6.vb)]  
  
## 请参阅  
 [匿名类型定义](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)   
 [如何：推断匿名类型声明中的属性名和类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)   
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)