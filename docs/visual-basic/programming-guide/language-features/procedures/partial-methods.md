---
title: "分部方法 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.PartialMethod"
  - "PartialMethod"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "插入到代码中的自定义逻辑 [Visual Basic]"
  - "将自定义逻辑插入到代码中"
  - "方法 [Visual Basic], 分部方法"
  - "分部方法 [Visual Basic]"
  - "分部, 方法 [Visual Basic]"
ms.assetid: 74b3368b-b348-44a0-a326-7d7dc646f4e9
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 分部方法 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过分部方法，开发人员可以将自定义逻辑插入代码中。  通常，代码是设计器生成的类的一部分。  分部方法在代码生成器所创建的分部类中定义，它们通常用于提供通知，指出某些内容已更改。  开发人员可以使用分部方法来指定对更改进行响应的自定义行为。  
  
 代码生成器的设计器仅定义方法签名和对方法的一个或多个调用。  这样，如果开发人员要自定义所生成的代码的行为，就可以为方法提供实现。  未提供任何实现时，编译器会移除对方法的调用，这样不会产生额外的性能开销。  
  
## 声明  
 生成的代码通过将关键字 `Partial` 放置在签名行的开头，对分部方法的定义进行标记。  
  
```vb#  
Partial Private Sub QuantityChanged()  
End Sub  
```  
  
 定义必须满足下面的条件：  
  
-   方法必须是 `Sub`，而不是 `Function`。  
  
-   方法的主体必须留空。  
  
-   访问修饰符必须为 `Private`。  
  
## 实现  
 实现主要由分部方法主体的内容构成。  实现通常在定义的独立分部类中，由要扩展生成代码的开发人员编写。  
  
```vb#  
Private Sub QuantityChanged()  
'    Code for executing the desired action.  
End Sub  
```  
  
 上一示例在声明中原封不动地重复签名，实际上是可以有所更改的。  具体说来，可以添加其他修饰符，例如 `Overloads` 或 `Overrides`。  只允许使用一个 `Overrides` 修饰符。  有关方法修饰符的更多信息，请参见 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)。  
  
## 使用  
 调用分部方法和调用任何其他 `Sub` 过程一样。  如果方法已经实现，则计算参数并执行方法主体。  但是，请记住，分部方法的实现是可选的。  如果方法未实现，则调用不起任何作用，也不会计算作为参数传递给方法的表达式。  
  
## 示例  
 在名为 Product.Designer.vb 的文件中，定义具有 `Quantity` 属性的 `Product` 类。  
  
 [!code-vb[VbVbalrPartialMeths#4](./codesnippet/VisualBasic/partial-methods_1.vb)]  
  
 在名为 Product.vb 的文件中，提供 `QuantityChanged` 的实现。  
  
 [!code-vb[VbVbalrPartialMeths#5](./codesnippet/VisualBasic/partial-methods_2.vb)]  
  
 最后，在项目的 Main 方法中，声明 `Product` 实例并为其 `Quantity` 属性提供初始值。  
  
 [!code-vb[VbVbalrPartialMeths#6](./codesnippet/VisualBasic/partial-methods_3.vb)]  
  
 应出现一个消息框，显示如下消息：  
  
 `Quantity was changed to 100`  
  
## 请参阅  
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [可选参数](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [分部](../../../../visual-basic/language-reference/modifiers/partial.md)   
 [LINQ to SQL 中的代码生成](../Topic/Code%20Generation%20in%20LINQ%20to%20SQL.md)   
 [使用分部方法添加业务逻辑](../Topic/Adding%20Business%20Logic%20By%20Using%20Partial%20Methods.md)