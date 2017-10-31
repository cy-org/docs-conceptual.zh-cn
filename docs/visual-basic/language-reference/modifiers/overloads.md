---
title: "Overloads (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Overloads"
  - "Overloads"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "按签名隐藏"
  - "Overloads 关键字"
  - "Shadows 关键字"
  - "签名, 隐藏依据"
ms.assetid: 0c6820b8-25b2-4664-bc59-5ca93c99c042
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Overloads (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定某一属性或过程重新声明一个或多个具有相同名称的现有属性或过程。  
  
## 备注  
 *“重载”*是为同一范围内的某个给定属性或过程名称提供多个定义的做法。  用不同的签名重新声明属性或过程有时称为*“按签名隐藏”*。  
  
## 规则  
  
-   **声明上下文。** 只能在属性或过程声明语句中使用 `Overloads`。  
  
-   **组合修饰符。** 不能在同一过程声明中将 `Overloads` 与 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md) 同时指定。  
  
-   **必需的不同点。** 在该声明中，*“签名”*必须与它重载的每个属性或过程的签名不同。  签名包含属性或过程名以及以下内容：  
  
    -   参数的数量  
  
    -   参数顺序  
  
    -   参数的数据类型  
  
    -   类型参数的数量（针对泛型过程）  
  
    -   返回类型（仅针对转换运算符过程）  
  
     所有重载都必须有相同的名称，但每个重载必须在上面的一个或多个方面与所有其他重载不同。  这使编译器在代码调用属性或过程时可以区分要使用哪个版本。  
  
-   **不允许的不同点。** 对于重载属性或过程而言，更改下面的一项或多项无效，因为它们不是签名的一部分：  
  
    -   它是否返回值（针对过程）  
  
    -   返回值的数据类型（除转换运算符之外）  
  
    -   参数或类型参数的名称  
  
    -   对类型参数的约束（针对泛型过程）  
  
    -   参数修饰符关键字（如 `ByRef` 或 `Optional`）  
  
    -   属性或过程修饰符关键字（如 `Public` 或 `Shared`）  
  
-   **可选修饰符。** 当在同一个类中定义多个重载属性或过程时，不必使用 `Overloads` 修饰符。  然而，如果在某个声明中使用 `Overloads`，则必须在所有的声明中使用它。  
  
-   **隐藏和重载。** `Overloads` 也可用于隐藏基类中的现有成员或一组重载成员。  以这种方式使用 `Overloads` 时，应使用与基类成员相同的名称和参数列表来声明属性或方法，并且不提供 `Shadows` 关键字。  
  
 如果使用 `Overrides`，编译器将隐式添加 `Overloads`，以便库 API 更轻松地使用 C\#。  
  
 `Overloads` 修饰符可用于下面的上下文中：  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [过程重载](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [如何：定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)