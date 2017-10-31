---
title: "Nothing (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Nothing"
  - "vb.Nothing"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Nothing 关键字"
  - "Nothing 关键字, 语法"
ms.assetid: 06176e2d-bbf7-4a37-afaa-a86ad21ee99f
caps.latest.revision: 31
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 31
---
# Nothing (Visual Basic)
[!INCLUDE[vs2017banner](../../visual-basic/includes/vs2017banner.md)]

表示任意数据类型的默认值。  对于引用类型，默认值为 `null` 引用。  对于值类型，默认值取决于值类型是否可以为 null 的。  
  
> [!NOTE]
>  对非可以为 null 的类型，在 Visual Basic 中 `Nothing` 与 c\# 的 `null` 不同。  在 Visual Basic 中，因此，如果您设置了不可为 null 的值类型的变量。 `Nothing`，变量设置为其声明类型的默认值。  在 c\# 中，，如果将一个非 null 值类型的变量赋给 `null`，将产生编译时错误。  
  
## 备注  
 `Nothing` 表示数据类型的默认值。  默认取决于该变量是否为值类型或引用类型。  
  
 *值类型的* 变量直接包含它的值。  值类型包括所有数值数据类型、 `Boolean`、 `Char`、 `Date`、所有结构以及所有枚举。  *引用类型的* 变量存储对对象的实例在内存中。  引用类型包括类、数组、委托和字符串。  有关更多信息，请参见 [值类型和引用类型](../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)。  
  
 如果变量是值类型， `Nothing` 行为取决于该变量是否是可以为 null 的数据类型。  若要表示可以为 null 值的类型，添加一个 `?` 修饰符到类型名称。  分配 `Nothing` 到一个可以为 null 的变量将值设置为 `null`。  有关更多信息和示例，请参见[可以为 Null 的值类型](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)。  
  
 如果变量不可为 null 的是值类型，分配 `Nothing` 为其设置为其声明类型的默认值。  如果该类型包含变量成员，则这些成员都会设置为其默认值。  下面的示例就标量类型对此进行了说明。  
  
 [!code-vb[VbVbalrKeywords#7](../../visual-basic/language-reference/codesnippet/VisualBasic/nothing_1.vb)]  
  
 如果变量是引用类型， `Nothing` 分配给变量设置为 `null` 引用变量的类型。  设置为 `null` 的变量引用不与任何对象。  下面的示例说明了这一点。  
  
 [!code-vb[VbVbalrKeywords#8](../../visual-basic/language-reference/codesnippet/VisualBasic/nothing_2.vb)]  
  
 当检查引用 \(或可以为 null 的值类型\) 时变量是否 `null`，不要使用 `= Nothing` 或 `<> Nothing`。  始终使用 `Is Nothing` 或 `IsNot Nothing`。  
  
 若要在 Visual Basic 的字符串，该空字符串相等 `Nothing`。  因此， `"" = Nothing` 为 true。  
  
 下面的示例演示使用 `Is` 和 `IsNot` 运算符的比较。  
  
 [!code-vb[VbVbalrKeywords#9](../../visual-basic/language-reference/codesnippet/VisualBasic/nothing_3.vb)]  
  
 如果您在不使用 `As` 子句的情况下声明一个变量，并将其设置为 `Nothing`，则变量将具有 `Object` 类型。  其示例为 `Dim something = Nothing`。  编译时错误发生在这种情况下，当 `Option Strict` 打开，而 `Option Infer` 关闭。  
  
 将 `Nothing` 赋给对象变量时，该变量将不再引用任何对象实例。  如果对象以前引用了一个实例，那么将其设置为 `Nothing` 不会终止该实例本身。  只有在垃圾回收器 \(GC\) 检测到没有任何剩余的活动的引用时，才会终止该实例，并释放与其关联的内存和系统资源。  
  
 `Nothing` 与 <xref:System.DBNull> 对象不同，表示一个未初始化的变量或不存在的数据库列。  
  
## 请参阅  
 [Dim 语句](../../visual-basic/language-reference/statements/dim-statement.md)   
 [对象生存期：如何创建和销毁对象](../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)   
 [Visual Basic 中的生存期](../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Is 运算符](../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot 运算符](../../visual-basic/language-reference/operators/isnot-operator.md)   
 [可以为 Null 的值类型](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)