---
title: "Out（泛型修饰符）(Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.VarianceOut"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "协变, Out 关键字 [Visual Basic]"
  - "Out 关键字 [Visual Basic]"
ms.assetid: c4418369-1518-4a46-9a1e-054c61038eca
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Out（泛型修饰符）(Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对于泛型类型参数，`Out` 关键字指定该类型是协变的。  
  
## 备注  
 通过协变，可以使用与泛型参数指定的派生类型相比，派生程度更大的类型。  这样可以对委托类型和实现变体接口的类进行隐式转换。  
  
 有关更多信息，请参见[协变和逆变](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 规则  
 可以在泛型接口和委托中使用 `Out` 关键字。  
  
 在泛型接口中，当符合下列条件时，可以将类型参数声明为是协变的。  
  
-   类型形参仅用作接口方法的返回类型，不用作方法实参的类型。  
  
    > [!NOTE]
    >  此规则有一个例外。  如果在协变接口中，包含用作方法参数的逆变泛型委托，则可以将协变类型用作此委托的泛型类型参数。  有关协变和逆变泛型委托的更多信息，请参见[委托中的变体](../Topic/Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)和[对 Func 和 Action 泛型委托使用变体](../Topic/Using%20Variance%20for%20Func%20and%20Action%20Generic%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)。  
  
-   类型参数不用作接口方法的泛型约束。  
  
 在泛型委托中，如果类型形参仅用作方法返回类型，而不用于方法实参，则可声明为协变的。  
  
 引用类型支持协变和逆变，但值类型不支持。  
  
 在 Visual Basic 中，只有在指定委托类型后，才能在协变接口中声明事件。  此外，协变接口不能有嵌套类、枚举或结构，但可以有嵌套接口。  
  
## 行为  
 如果接口具有协变类型形参，则允许其方法返回与接口类型形参指定的派生类型相比，派生程度更大的类型的实参。  例如，由于在 .NET Framework 4 的 <xref:System.Collections.Generic.IEnumerable%601> 接口中，类型 T 是协变的，因此无需使用任何特殊转换方法就可以将 `IEnumerabe(Of String)` 类型的对象分配给 `IEnumerable(Of Object)` 类型的对象。  
  
 可以向协变委托分配同一类型的其他委托，但需使用派生程度较大的泛型类型参数。  
  
## 示例  
 下例演示如何声明、扩展和实现一个协变泛型接口。  此外还演示了如何对实现协变接口的类使用隐式转换。  
  
 [!code-vb[vbVarianceKeywords#3](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/out-generic-modifier_1.vb)]  
  
## 示例  
 下例演示如何声明、实例化和调用一个协变泛型委托。  此外，该示例还演示如何对委托类型使用隐式转换。  
  
 [!code-vb[vbVarianceKeywords#4](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/out-generic-modifier_2.vb)]  
  
## 请参阅  
 [泛型接口中的变体](../Topic/Variance%20in%20Generic%20Interfaces%20\(C%23%20and%20Visual%20Basic\).md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)