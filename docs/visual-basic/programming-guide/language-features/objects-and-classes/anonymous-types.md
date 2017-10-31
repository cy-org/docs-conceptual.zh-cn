---
title: "匿名类型 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AnonymousType"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "匿名类型 [Visual Basic]"
  - "匿名类型 [Visual Basic], 关于匿名类型"
  - "类型 [Visual Basic], 匿名"
ms.assetid: 7b87532c-4b3e-4398-8503-6ea9d67574a4
caps.latest.revision: 46
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 46
---
# 匿名类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

Visual Basic 支持匿名类型，使您能够在不为数据类型编写类定义的情况下创建对象。  此时，编译器将为您生成类。  该类没有可用的名称，是直接从 <xref:System.Object> 继承的，它包含在声明对象时指定的属性。  由于未指定数据类型的名称，因此将它称为“匿名类型”。  
  
 下面的示例声明并创建变量 `product`，作为具有两个属性（`Name` 和 `Price`）的匿名类型的实例。  
  
 [!code-vb[VbVbalrAnonymousTypes#1](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_1.vb)]  
  
 查询表达式使用匿名类型将查询所选择的数据列组合在一起。  由于不能预测特定查询可能选择的列，因此不能提前定义结果的类型。  使用匿名类型可以编写以任何顺序选择任意个列的查询。  编译器创建与指定属性和指定顺序匹配的数据类型。  
  
 在下面的示例中，`products` 是产品对象列表，其中每个对象都有多个属性。  变量 `namePriceQuery` 保存查询的定义，该查询在执行时，返回具有两个属性（`Name` 和 `Price`）的匿名类型的实例集合。  
  
 [!code-vb[VbVbalrAnonymousTypes#2](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_2.vb)]  
  
 变量 `nameQuantityQuery` 保存查询的定义，该查询在执行时，返回具有两个属性（`Name` 和 `OnHand`）的匿名类型的实例集合。  
  
 [!code-vb[VbVbalrAnonymousTypes#3](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_3.vb)]  
  
 有关编译器为匿名类型创建的代码的更多信息，请参见[匿名类型定义](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)。  
  
> [!CAUTION]
>  匿名类型的名称由编译器生成，并可能随编译的不同而不同。  代码不应使用或依赖匿名类型的名称，因为重新编译项目时该名称可能更改。  
  
## 声明匿名类型  
 匿名类型实例的声明使用初始值设定项列表来指定类型的属性。  在声明匿名类型时可以只指定属性，而不指定方法或事件等其他类元素。  在下面的示例中，`product1` 是具有两个属性（`Name` 和 `Price`）的匿名类型的实例。  
  
 [!code-vb[VbVbalrAnonymousTypes#4](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_4.vb)]  
  
 如果将属性指定为主要属性，则可以使用它们来比较两个匿名类型实例是否相等。  不过，主要属性的值是不能更改的。  有关更多信息，请参见本主题后面的“主要属性”一节。  
  
 请注意，声明匿名类型的实例与使用对象初始值设定项声明命名类型的实例相似。  
  
 [!code-vb[VbVbalrAnonymousTypes#5](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_5.vb)]  
  
 有关指定匿名类型属性的其他方式的更多信息，请参见[如何：推断匿名类型声明中的属性名和类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)。  
  
## 主要属性  
 主要属性与非主要属性在多个重要方面存在差别：  
  
-   只在确定两个实例是否相等时才比较主要属性的值。  
  
-   主要属性的值是只读的，不能更改。  
  
-   对于匿名类型，编译器生成的哈希代码算法中只包含主要属性值。  
  
### 相等  
 匿名类型的实例仅当是相同匿名类型的实例时才相等。  如果两个实例满足下面的条件，则编译器将它们视为相同类型的实例：  
  
-   在相同的程序集中声明。  
  
-   其属性具有相同的名称、相同的推断类型并且以相同顺序声明。  名称比较不区分大小写。  
  
-   每个实例的相同属性都标记为主要属性。  
  
-   每个声明中至少有一个属性是主要属性。  
  
 没有主要属性的匿名类型的实例只等于它自身。  
  
 [!code-vb[VbVbalrAnonymousTypes#6](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_6.vb)]  
  
 相同匿名类型的两个实例在其主要属性的值相等时相等。  下面的示例演示如何测试是否相等。  
  
 [!code-vb[VbVbalrAnonymousTypes#7](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_7.vb)]  
  
### 只读值  
 主要属性的值是不能更改的。  例如，在前面示例的 `prod8` 中，`Name` 和 `Price` 为 `read-only` 字段，但 `OnHand` 是可以更改的。  
  
 [!code-vb[VbVbalrAnonymousTypes#8](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_8.vb)]  
  
## 查询表达式中的匿名类型  
 查询表达式并不总是要求创建匿名类型。  只要可能，它们就使用现有类型来保存列数据。  当查询返回数据源的全部记录，或只返回每条记录的一个字段时，会出现这种情况。  在下面的代码示例中，`customers` 是 `Customer` 类的对象的集合。  该类有很多属性，在查询结果中，可以以任意顺序包含一个或多个属性。  在最开始的两个示例中，不需要匿名类型，因为查询选择命名类型的元素。  
  
-   `custs1` 包含字符串集合，因为 `cust.Name` 是字符串。  
  
     [!code-vb[VbVbalrAnonymousTypes#30](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_9.vb)]  
  
-   `custs2` 包含 `Customer` 对象的集合，因为 `customers` 的每个元素都是 `Customer` 对象，并且整个元素都由查询选择。  
  
     [!code-vb[VbVbalrAnonymousTypes#31](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_10.vb)]  
  
 但是，相应的命名类型并非始终可用。  出于特定目的，可能希望执行以下操作：一，选择客户的名称和地址；二，选择客户 ID 号和位置；三，选择客户的名称、地址和订单历史。  使用匿名类型可以选择任意顺序的属性组合，而无需事先声明新的命名类型来保存结果。  相反，编译器会为每次属性编译创建匿名类型。  下面的查询从 `customers` 中的每个 `Customer` 对象中只选择客户的名称和 ID 号。  因此，编译器会创建仅包含这两个属性的匿名类型。  
  
 [!code-vb[VbVbalrAnonymousTYpes#32](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_11.vb)]  
  
 匿名类型的属性的名称和数据类型都取自 `Select` 的参数 `cust.Name` 和 `cust.ID`。  查询所创建的匿名类型的属性始终是主要属性。  在下面的 `For Each` 循环中执行 `custs3` 时，结果是具有两个主要属性（`Name` 和 `ID`）的匿名类型的实例集合。  
  
 [!code-vb[VbVbalrAnonymousTypes#33](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_12.vb)]  
  
 `custs3` 所表示的集合中的元素是强类型的，可以使用 IntelliSense 浏览可用属性和确认其类型。  
  
 有关更多信息，请参见 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)。  
  
## 确定是否使用匿名类型  
 在创建匿名类实例形式的对象之前，请考虑匿名类型是否为最佳选择。  例如，如果要创建临时对象来包含相关数据，也不需要完整类可能包含的其他字段和方法，匿名类型就是很好的解决方案。  如果每个声明都需要不同的属性选择，或者要更改属性顺序，则适于使用匿名类型。  但是，如果项目以固定顺序包括多个具有相同属性的对象，则使用具有类构造函数的命名类型来声明它们可能更为方便。  例如，使用相应的构造函数，声明 `Product` 类的多个实例比声明匿名类型的多个实例更方便。  
  
 [!code-vb[VbVbalrAnonymousTypes#9](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_13.vb)]  
  
 命名类型的另一优点是编译器可以捕获属性名称的无意拼写错误。  在前面的示例中，`firstProd2`、`secondProd2` 和 `thirdProd2` 应为相同匿名类型的实例。  但是，如果使用下面的一种方式意外地声明了 `thirdProd2`，其类型将不同于 `firstProd2` 和 `secondProd2` 的类型。  
  
 [!code-vb[VbVbalrAnonymousTypes#10](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-types_14.vb)]  
  
 更重要的是，对于未应用于命名类型实例的匿名类型，在使用上会有很多限制。  `firstProd2`、`secondProd2` 和 `thirdProd2` 是具有相同匿名类型的实例。  但是，共享匿名类型的名称不可用，不能在代码中出现在需要使用类型名称的位置。  例如，匿名类型不能用来定义方法签名，不能用来声明其他变量或字段，也不能用在任何类型声明中。  因此，如果必须在方法间共享信息，则不适合使用匿名类型。  
  
## 匿名类型定义  
 在响应匿名类型的实例声明时，编译器创建一个包含指定属性的新类定义。  
  
 如果匿名类型至少包含一个主要属性，则定义将重写三个从 <xref:System.Object> 继承的成员：<xref:System.Object.Equals%2A>、<xref:System.Object.GetHashCode%2A> 和 <xref:System.Object.ToString%2A>。  生成来测试相等性和确定哈希代码值的代码仅考虑主要属性。  如果匿名类型不包含主要属性，则仅重写 <xref:System.Object.ToString%2A>。  匿名类型的显式命名属性不能与这些生成的方法冲突。  也就是说，不能使用 `.Equals`、`.GetHashCode` 或 `.ToString` 来命名属性。  
  
 此外，至少具有一个主要属性的匿名类型定义还实现 <xref:System.IEquatable%601?displayProperty=fullName> 接口，其中 `T` 是匿名类型的类型。  
  
 有关编译器所创建的代码和重写方法的功能的更多信息，请参见[匿名类型定义](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)。  
  
## 请参阅  
 [对象初始值设定项：命名类型和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [如何：推断匿名类型声明中的属性名和类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)   
 [匿名类型定义](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)   
 [Key](../../../../visual-basic/language-reference/modifiers/key.md)