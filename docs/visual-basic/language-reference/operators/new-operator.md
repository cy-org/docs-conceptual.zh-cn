---
title: "New 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.new"
  - "vb.NewConstraint"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "约束, New 关键字"
  - "约束, Visual Basic 泛型类型"
  - "泛型 [Visual Basic], 约束"
  - "New 约束"
  - "New 关键字"
ms.assetid: d7d566d7-fe0e-4336-91f7-641a542de4d0
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# New 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

引入 `New` 子句以创建一个新的对象实例，在类型参数上指定构造函数条件，或者将 `Sub` 过程识别为构造函数。  
  
## 备注  
 在声明或赋值语句中，`New` 子句必须指定一个可从中创建实例的已定义类。  这意味着该类必须公开调用代码可以访问的一个或多个构造函数。  
  
 可以在声明语句或赋值语句中使用 `New` 子句。  该语句在运行时将调用指定类的相应构造函数，传递您提供的所有参数。  下面的示例对此进行了演示，它创建了具有两个构造函数（一个不采用参数，另一个采用字符串参数）的 `Customer` 类的实例。  
  
 [!code-vb[VbVbalrKeywords#11](../../../visual-basic/language-reference/codesnippet/VisualBasic/new-operator_1.vb)]  
  
 因为数组也是类，所以 `New` 可以创建新的数组实例，如下面的示例所示。  
  
 [!code-vb[VbVbalrKeywords#12](../../../visual-basic/language-reference/codesnippet/VisualBasic/new-operator_2.vb)]  
  
 如果内存不足，无法创建新的实例，公共语言运行时 \(CLR\) 将引发 <xref:System.OutOfMemoryException> 错误。  
  
> [!NOTE]
>  `New` 关键字还在类型参数列表中使用，以指定提供的类型必须公开可访问的无参数构造函数。  有关类型参数和约束的更多信息，请参见[类型列表](../../../visual-basic/language-reference/statements/type-list.md)。  
  
 若要为类创建构造函数过程，请将 `Sub` 过程的名称设为 `New` 关键字。  有关更多信息，请参见 [对象生存期：如何创建和销毁对象](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)。  
  
 `New` 关键字可用于下面的上下文中：  
  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Of](../../../visual-basic/language-reference/statements/of-clause.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 <xref:System.OutOfMemoryException>   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [类型列表](../../../visual-basic/language-reference/statements/type-list.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [对象生存期：如何创建和销毁对象](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)