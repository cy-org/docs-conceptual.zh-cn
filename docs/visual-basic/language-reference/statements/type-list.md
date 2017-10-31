---
title: "类型列表 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "StructureConstraint"
  - "vb.StructureConstraint"
  - "ClassConstraint"
  - "vb.ClassConstraint"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "class 约束"
  - "约束, Class 关键字"
  - "约束, 在类型参数中"
  - "约束, Structure 关键字"
  - "约束, Visual Basic 泛型类型"
  - "泛型参数"
  - "泛型 [Visual Basic], 约束"
  - "泛型 [Visual Basic], 泛型类型"
  - "泛型 [Visual Basic], 类型列表"
  - "泛型 [Visual Basic], 类型参数"
  - "参数, 泛型"
  - "参数, 类型"
  - "结构约束"
  - "类型参数"
  - "类型参数, 约束"
  - "类型 [Visual Basic], 泛型"
ms.assetid: 56db947a-2ae8-40f2-a70a-960764e9d0db
caps.latest.revision: 33
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 33
---
# 类型列表 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定泛型编程元素的类型参数。  以逗号分隔多个参数。  以下为一个类型参数的语法。  
  
## 语法  
  
```  
  
[genericmodifier] typename [ As constraintlist ]  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`genericmodifier`|可选。  只能在泛型接口和委托中使用。  可以通过使用 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md) 关键字声明类型协变，或者通过使用 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md) 关键字声明类型逆变。  请参见 [协变和逆变](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)。|  
|`typename`|必选。  类型参数的名称。  这是一个占位符，将替换为相应的类型参数所提供的已定义类型。|  
|`constraintlist`|可选。  要求列表，用于约束可提供给 `typename` 的数据类型。  如果拥有多个约束，请将它们置于大括号 \(`{ }`\) 内并用逗号分隔各约束。  您必须使用 [As](../../../visual-basic/language-reference/statements/as-clause.md) 关键字引入约束列表。  `As` 关键字只能在列表的起始处使用一次。|  
  
## 备注  
 每个泛型编程元素必须至少获取一个类型参数。  类型参数为客户端代码在创建泛型类型的实例时指定的某一特定类型（构造元素）的占位符。  您可以定义泛型类、结构、接口、过程或委托。  
  
 有关何时定义泛型类型的更多信息，请参见 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)。  有关类型参数名称的更多信息，请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
## 规则  
  
-   **括号。**如果您提供了一份类型参数列表，必须将其置于括号内，并且必须使用 [Of](../../../visual-basic/language-reference/statements/of-clause.md) 关键字引入此列表。  `Of` 关键字只能在列表的起始处使用一次。  
  
-   **约束。**类型参数中的约束列表可以包括以下项目的任意组合：  
  
    -   任何数目的接口。  提供的类型必须实现此列表中的每个接口。  
  
    -   最多为一个类。  提供的类型必须继承自该类。  
  
    -   `New` 关键字。  提供的类型必须公开泛型类型可以访问的无参数构造函数。  这一点在使用一个或多个接口约束类型参数时非常有用。  实现接口的类型不必公开构造函数，并且受构造函数的访问级别限制，泛型类型中的代码可能无法访问该构造函数。  
  
    -   `Class` 关键字或 `Structure` 关键字。  `Class` 关键字约束泛型类型形参，以要求传递给它的任何类型实参都是引用类型（例如字符串、数组或委托）或者从类创建的对象。  `Structure` 关键字约束泛型类型形参，以要求传递给它的任何类型实参都是值类型（例如结构、枚举）或基本数据类型。  不能在同一个 `constraintlist` 中同时包括 `Class` 和 `Structure`。  
  
     提供的类型必须符合 `constraintlist` 中的每一个要求。  
  
     每个类型参数中的约束均独立于其他类型参数中的约束。  
  
## 行为  
  
-   **编译时替换。**根据泛型编程元素创建构造类型时，应为每个类型参数提供一个已定义的类型。  Visual Basic 编译器将泛型元素中 `typename` 的每一个匹配项都替换为提供的类型。  
  
-   **缺少约束。**如果类型参数中未指定任何约束，代码将只限于受该类型参数的 [Object 数据类型](../../../visual-basic/language-reference/data-types/object-data-type.md)支持的操作和成员。  
  
## 示例  
 下面的示例演示泛型字典类的主干定义，其中包括将新条目添加到字典中的主干函数。  
  
 [!code-vb[VbVbalrStatements#3](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/type-list_1.vb)]  
  
## 示例  
 由于 `dictionary` 为泛型，因此使用它的代码可以根据它创建多种对象，创建的每种对象都具有相同的功能，但却作用于不同的数据类型。  下面的示例显示一行代码，该代码将创建一个 `dictionary` 对象，该对象具有 `String` 项和 `Integer` 键。  
  
 [!code-vb[VbVbalrStatements#4](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/type-list_2.vb)]  
  
## 示例  
 下面的示例显示由上述示例生成的等效主干定义。  
  
 [!code-vb[VbVbalrStatements#5](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/type-list_3.vb)]  
  
## 请参阅  
 [Of](../../../visual-basic/language-reference/statements/of-clause.md)   
 [New 运算符](../../../visual-basic/language-reference/operators/new-operator.md)   
 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Object 数据类型](../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [如何：使用泛型类](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [协变和逆变](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)