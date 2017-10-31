---
title: "Is 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.is"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "比较运算符"
  - "等效对象"
  - "Is 运算符 [Visual Basic]"
  - "TypeOf...Is 表达式"
ms.assetid: 8045a6c8-2a83-45b6-ad47-d09a704c656d
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Is 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

比较两个对象引用变量。  
  
## 语法  
  
```  
  
result = object1 Is object2  
```  
  
## 部件  
 `result`  
 必选。  任何 `Boolean` 值。  
  
 `object1`  
 必选。  任何 `Object` 名称。  
  
 `object2`  
 必选。  任何 `Object` 名称。  
  
## 备注  
 `Is` 运算符确定两个对象引用是否引用同一个对象。  但是，它不执行值比较。  如果 `object1` 和 `object2` 引用同一个对象实例，则 `result` 为 `True`；如果它们不引用同一个对象，则 `result` 为 `False`。  
  
 还可以将 `Is` 与 `TypeOf` 关键字一起使用，以组成 `TypeOf`...`Is` 表达式，此表达式测试对象变量是否与数据类型兼容。  
  
> [!NOTE]
>  `Is` 关键字还在 [Select...Case 语句](../../../visual-basic/language-reference/statements/select-case-statement.md) 中使用。  
  
## 示例  
 下面的示例使用 `Is` 运算符比较对象引用对。  结果赋值为 `Boolean` 值，它表示两个对象是否相同。  
  
 [!code-vb[VbVbalrOperators#27](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/is-operator_1.vb)]  
  
 如前面的示例所演示的一样，可以使用 `Is` 运算符测试早期绑定对象和后期绑定对象。  
  
## 请参阅  
 [TypeOf 运算符](../../../visual-basic/language-reference/operators/typeof-operator.md)   
 [IsNot 运算符](../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [比较运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)