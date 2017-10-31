---
title: "In（泛型修饰符）(Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.VarianceIn"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "逆变, In 关键字 [Visual Basic]"
  - "In 关键字 [Visual Basic]"
ms.assetid: 59bb13c5-fe96-42b8-8286-86293d1661c5
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# In（泛型修饰符）(Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对于泛型类型参数，`In` 关键字指定该类型参数是逆变的。  
  
## 备注  
 通过逆变，可以使用与泛型参数指定的派生类型相比，派生程度更小的类型。  这样可以对委托类型和实现变体接口的类进行隐式转换。  
  
 有关更多信息，请参见[协变和逆变](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 规则  
 可以在泛型接口和委托中使用 `In` 关键字。  
  
 如果类型形参仅用作方法实参类型，而不用作方法返回类型，则可以在泛型接口或委托中将该形参声明为逆变形参。 形参不能是协变或逆变形参。  `ByRef` 参数不能是协变或逆变的。  
  
 引用类型支持协变和逆变，而值类型不支持。  
  
 在 Visual Basic 中，只有在指定委托类型后，才能在逆变接口中声明事件。  此外，逆变接口不能有嵌套类、枚举或结构，但可以有嵌套接口。  
  
## 行为  
 如果接口具有逆变类型形参，则允许其方法接受与接口类型形参指定的派生类型相比，派生程度更小的类型的实参。  例如，由于在 .NET Framework 4 的 <xref:System.Collections.Generic.IComparer%601> 接口中，类型 T 是逆变的，因此如果 `Person` 继承 `Employee`，则无需使用任何特殊转换方法，就可以将 `IComparer(Of Person)` 类型的对象指派给 `IComparer(Of Employee)` 类型的对象。  
  
 可以向逆变委托分配同一类型的其他委托，但需使用派生程度较小的泛型类型参数。  
  
## 示例  
 下例演示如何声明、扩展和实现一个逆变泛型接口。  此外还演示了如何对实现此接口的类使用隐式转换。  
  
 [!code-vb[vbVarianceKeywords#1](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/in-generic-modifier_1.vb)]  
  
## 示例  
 下例演示如何声明、实例化和调用一个逆变泛型委托。  此外还演示了如何隐式转换委托类型。  
  
 [!code-vb[vbVarianceKeywords#2](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/in-generic-modifier_2.vb)]  
  
## 请参阅  
 [泛型接口中的变体](../Topic/Variance%20in%20Generic%20Interfaces%20\(C%23%20and%20Visual%20Basic\).md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)