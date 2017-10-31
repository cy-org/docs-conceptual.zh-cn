---
title: "Overrides (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Overrides"
  - "vb.Overrides"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Overrides 关键字"
  - "重写"
  - "重写, Overrides 关键字"
  - "过程, 重写"
  - "过程, 重新定义"
  - "属性 [Visual Basic], 重写"
  - "属性 [Visual Basic], 重新定义"
ms.assetid: 9f5e6144-ce10-465e-842b-1a8f8760af90
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Overrides (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定某一属性或过程可重写从基类中继承的具有相同名称的属性或过程。  
  
## 备注  
  
## 规则  
  
-   **声明上下文。** 只能在属性或过程声明语句中使用 `Overrides`。  
  
-   **组合修饰符。** 不能在同一过程声明中同时指定 `Overrides` 和 `Shadows` 或 `Shared`。  由于重写元素是隐式可重写的，因此不能将 `Overridable` 与 `Overrides` 组合到一起。  
  
-   **匹配签名。** 此声明的签名必须与其重写的属性或过程的*签名*完全匹配。  这意味着参数列表必须具有相同数量的参数，并且排序顺序和数据类型都必须完全相同。  
  
     除签名外，重写的声明还必须完全匹配以下项：  
  
    -   访问级别  
  
    -   返回类型（如有）  
  
-   **泛型签名。** 对于泛型过程，签名包括类型参数的数量。  因此，重写的声明必须在这方面与基类版本匹配。  
  
-   **附加匹配。** 除匹配基类版本的签名外，此声明还必须在以下方面与其匹配：  
  
    -   访问级别修饰符（例如 [Public](../../../visual-basic/language-reference/modifiers/public.md)）  
  
    -   传递每个参数的机制（[ByVal](../../../visual-basic/language-reference/modifiers/byval.md) 或 [ByRef](../../../visual-basic/language-reference/modifiers/byref.md)）  
  
    -   泛型过程的每个类型参数的约束列表  
  
-   **隐藏和重写操作。** 隐藏和重写操作都可重新定义继承的元素，但这两种方法之间又具有很大的差异。  有关详细信息，请参阅[Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)。  
  
 如果使用 `Overrides`，编译器将隐式添加 `Overloads`，以便库 API 更轻松地使用 C\#。  
  
 `Overrides` 修饰符可用于下面的上下文中：  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)   
 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)   
 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [类型列表](../../../visual-basic/language-reference/statements/type-list.md)