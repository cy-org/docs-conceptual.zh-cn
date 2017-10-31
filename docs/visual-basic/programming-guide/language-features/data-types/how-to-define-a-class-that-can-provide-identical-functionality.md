---
title: "如何：定义可对不同数据类型提供相同功能的类 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据类型参数, 使用"
  - "类型形参, 定义"
  - "数据类型参数, 定义"
  - "参数 [Visual Basic], 数据类型"
  - "Of 关键字, 使用"
  - "约束, Visual Basic 泛型类型"
  - "泛型参数"
  - "数据类型参数"
  - "数据类型参数, 使用"
  - "泛型 [Visual Basic], 使用类型形参定义类"
  - "数据类型 [Visual Basic], 作为参数"
  - "数据类型 [Visual Basic], 作为参数"
  - "参数, 类型"
  - "类型参数"
  - "类型 [Visual Basic], 泛型"
  - "参数, 泛型"
  - "类型参数"
  - "数据类型参数"
  - "参数, 数据类型"
  - "泛型 [Visual Basic], 定义泛型类型"
  - "数据类型参数, 定义"
  - "类型实参, 定义"
  - "参数 [Visual Basic], 类型"
ms.assetid: a914adf8-e68f-4819-a6b1-200d1cf1c21c
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 29
---
# 如何：定义可对不同数据类型提供相同功能的类 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

你可以定义这样一个类：你可以通过该类创建可在不同数据类型上提供相同功能的对象。 为此，你可以在定义中指定一个或多个*类型形参*。 然后，该类将能够充当使用不同数据类型的对象的模板。 通过这种方式定义的类称为*泛型类*。  
  
 定义泛型类这种做法的优点在于：你只需定义一次泛型类，代码便可以利用它来创建使用各种数据类型的多个对象。 相对于使用 `Object` 类型定义类而言，这样做的性能将会更好。  
  
 除了类之外，你还可以定义和使用泛型结构、接口、过程和委托。  
  
### 使用类型形参定义类  
  
1.  采用常规方式定义类。  
  
2.  直接在类名称之后添加 `(Of`*typeparameter*`)`，以指定一个类型形参。  
  
3.  如果有一个以上的类型形参，请在括号内列出这些参数（以逗号分隔）。 不要重复 `Of` 关键字。  
  
4.  如果代码是对类型形参执行操作，而不是简单的赋值，请在该类型形参后添加一个 `As` 子句，以便添加一个或多个*约束*。 约束可保证为该类型形参提供的类型满足如下所示的要求：  
  
    -   支持代码执行的运算（如 `>`）  
  
    -   支持代码访问的成员（如方法）  
  
    -   公开无参数构造函数  
  
     如果未指定任何约束，则代码只能使用 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md) 支持的那些运算和成员。 有关详细信息，请参阅[类型列表](../../../../visual-basic/language-reference/statements/type-list.md)。  
  
5.  标识要使用所提供类型声明的每个类成员，然后将其声明为 `As` `typeparameter`。 这适用于内部存储、过程参数和返回值。  
  
6.  确保代码只使用它可提供给 `itemType` 的任何数据类型所支持的运算和方法。  
  
     下面的示例定义了一个类，用于管理一个非常简单的列表。 它将列表保存在内部数组 `items` 中，并且使用代码可声明列表元素的数据类型。 参数化构造函数允许使用代码设置 `items` 的上限，默认构造函数将此上限设置为 9（总共 10 项）。  
  
     [!code-vb[VbVbalrDataTypes#7](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/how-to-define-a-class-that-can-provide-identical-functionality_1.vb)]  
  
     你可以声明来自 `simpleList` 的一个类来保存 `Integer` 值的列表，声明另一个类来保存 `String` 值的列表，再声明一个类来保存 `Date` 值。 除了列表成员的数据类型外，依据所有这些类创建的对象的行为方式都相同。  
  
     所用代码提供给 `itemType` 的类型实参可以是内部类型（如 `Boolean` 或 `Double`）、结构、枚举或任何类型的类，包括应用程序定义的类。  
  
     可以使用以下代码测试类 `simpleList`。  
  
     [!code-vb[VbVbalrDataTypes#8](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/how-to-define-a-class-that-can-provide-identical-functionality_2.vb)]  
  
## 请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md)   
 [Of](../../../../visual-basic/language-reference/statements/of-clause.md)   
 [类型列表](../../../../visual-basic/language-reference/statements/type-list.md)   
 [如何：使用泛型类](../../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)