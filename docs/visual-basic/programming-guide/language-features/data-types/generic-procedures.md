---
title: "Visual Basic 中的泛型过程 | Microsoft Docs"
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
  - "泛型方法"
  - "泛型方法, 类型推理"
  - "泛型过程"
  - "泛型过程, 类型推理"
  - "泛型 [Visual Basic], 过程"
  - "泛型 [Visual Basic], 类型推理"
  - "过程, 泛型"
  - "类型推理"
  - "类型推理, 泛型"
ms.assetid: 95577b28-137f-4d5c-a149-919c828600e5
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Visual Basic 中的泛型过程
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

*“泛型过程”*，也称为*“泛型方法”*，是用至少一种类型参数定义的过程。  调用代码每次调用该过程时，都可根据其需要修改数据类型。  
  
 一个过程之所以成为泛型过程，并不是简单地由于在泛型类或泛型结构中进行定义。  若要成为泛型过程，除了可能采用的所有普通参数外，该过程还必须采用至少一种类型参数。  泛型类或泛型结构中可以包含非泛型过程；而非泛型类、结构或模块中也可以包含泛型过程。  
  
 泛型过程可以在它的普通参数列表、返回类型（如果有）和过程代码中使用其类型参数。  
  
## 类型推断  
 可以调用泛型过程，而不需提供任何类型变量。  如果以这种方式调用该过程，编译器将尝试确定传递到该过程类型变量中的相应数据类型。  这称为*“类型推理”*。  下面的代码演示一个调用，编译器推断它会将类型 `String` 传递给类型参数 `t`。  
  
 [!code-vb[VbVbalrDataTypes#15](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/generic-procedures_1.vb)]  
  
 如果编译器无法从调用的上下文中推断出类型变量，则将报告错误。  此类错误的一种可能原因是数组秩不匹配。  例如，假设您将一个普通参数定义为类型参数的数组。  如果所调用的泛型过程具有不同秩（维数）的数组，则秩不匹配将导致类型推理失败。  下面的代码演示一个调用，其中，二维数组被传递到需要一维数组的过程中。  
  
 `Public Sub demoSub(Of t)(ByVal arg() As t)`  
  
 `End Sub`  
  
 `Public Sub callDemoSub()`  
  
 `Dim twoDimensions(,) As Integer`  
  
 `demoSub(twoDimensions)`  
  
 `End Sub`  
  
 只需省略所有类型变量，即可调用类型推理。  如果您提供了一种类型变量，就必须提供所有类型变量。  
  
 只有泛型过程才支持类型推理。  无法对泛型类、泛型结构、泛型接口或泛型委托调用类型推理。  
  
## 示例  
  
### 说明  
 下面的示例定义了泛型 `Function` 过程，用于查找数组中的特定元素。  它定义一个类型参数，并用该类型参数在参数列表中构造两个参数。  
  
### 代码  
 [!code-vb[VbVbalrDataTypes#14](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/generic-procedures_2.vb)]  
  
### 注释  
 在上例中，需要能够将 `searchValue` 与 `searchArray` 中的每个元素进行比较。  为保证具有此能力，上例约束类型参数 `T` 实现 <xref:System.IComparable%601> 接口。  代码使用 <xref:System.IComparable%601.CompareTo%2A> 方法取代 `=` 运算符，这是因为无法保证为 `T` 提供的类型变量支持 `=` 运算符。  
  
 可以用下面的代码测试 `findElement` 过程。  
  
 [!code-vb[VbVbalrDataTypes#13](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/generic-procedures_3.vb)]  
  
 以前对 `MsgBox` 的调用分别显示“0”、“1”和“\-1”。  
  
## 请参阅  
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [如何：定义可对不同数据类型提供相同功能的类](../../../../visual-basic/programming-guide/language-features/data-types/how-to-define-a-class-that-can-provide-identical-functionality.md)   
 [如何：使用泛型类](../../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [类型列表](../../../../visual-basic/language-reference/statements/type-list.md)   
 [参数列表](../../../../visual-basic/language-reference/statements/parameter-list.md)