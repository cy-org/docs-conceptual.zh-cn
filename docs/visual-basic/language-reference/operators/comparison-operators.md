---
title: "比较运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.<>"
  - "vb.>="
  - "vb.<="
  - "vb.>"
  - "vb.<"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "< 运算符 [Visual Basic]"
  - "<= 运算符 [Visual Basic]"
  - "<> 运算符 [Visual Basic]"
  - "= 运算符 [Visual Basic]"
  - "> 运算符 [Visual Basic]"
  - ">= 运算符 [Visual Basic]"
  - "比较值 [Visual Basic]"
  - "比较运算符, Visual Basic"
  - "等于运算符 [Visual Basic]"
  - "大于运算符 [Visual Basic]"
  - "大于或等于运算符 [Visual Basic]"
  - "Is 运算符 [Visual Basic]"
  - "小于运算符 [Visual Basic]"
  - "小于或等于运算符 [Visual Basic]"
  - "Like 运算符 [Visual Basic]"
  - "不等于比较运算符 [Visual Basic]"
  - "运算符 [Visual Basic], 比较"
  - "运算符 [Visual Basic], 关系的"
  - "关系运算符, 语法"
  - "字符串比较 [Visual Basic]"
  - "symbols, 运算符"
ms.assetid: d6cb12a8-e52e-46a7-8aaf-f804d634a825
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 比较运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

以下是在 Visual Basic 中定义的比较运算符。  
  
 `<` 运算符  
  
 `<=` 运算符  
  
 `>` 运算符  
  
 `>=` 运算符  
  
 `=` 运算符  
  
 `<>` 运算符  
  
 [Is 运算符](../../../visual-basic/language-reference/operators/is-operator.md)  
  
 [IsNot 运算符](../../../visual-basic/language-reference/operators/isnot-operator.md)  
  
 [Like 运算符](../../../visual-basic/language-reference/operators/like-operator.md)  
  
 这些运算符比较两个表达式以确定它们是否相等，如果不相等，则确定它们之间的区别。  `Is`、`IsNot` 和 `Like` 在不同的“帮助”页中详细讨论。  此页中详细讨论关系比较运算符。  
  
## 语法  
  
```  
  
      result = expression1 comparisonoperator expression2  
result = object1 [Is | IsNot] object2  
result = string Like pattern  
```  
  
## 部件  
 `result`  
 必选。  `Boolean` 值，表示比较的结果。  
  
 `expression`  
 必选。  任何表达式。  
  
 `comparisonoperator`  
 必选。  任何关系比较运算符。  
  
 `object1`, `object2`  
 必选。  任何引用对象名称。  
  
 `string`  
 必选。  任何 `String` 表达式。  
  
 `pattern`  
 必选。  任何 `String` 表达式或字符范围。  
  
## 备注  
 下表列出了关系比较运算符以及判定 `result` 是为 `True` 还是为 `False` 的条件。  
  
|运算符|如果满足此条件，则为`True`|如果满足此条件，则为`False`|  
|---------|----------------------|-----------------------|  
|`<`（小于）|`expression1` \< `expression2`|`expression1` \>\= `expression2`|  
|`<=`（小于或等于）|`expression1` \<\= `expression2`|`expression1` 大于 `expression2`|  
|`>`（大于）|`expression1` 大于 `expression2`|`expression1` \<\= `expression2`|  
|`>=`（大于或等于）|`expression1` \>\= `expression2`|`expression1` \< `expression2`|  
|`=`（等于）|`expression1` \= `expression2`|`expression1` \<\> `expression2`|  
|`<>`（不等于）|`expression1` \<\> `expression2`|`expression1` \= `expression2`|  
  
> [!NOTE]
>  [\= 运算符](../../../visual-basic/language-reference/operators/assignment-operator.md) 也用作赋值运算符。  
  
 `Is` 运算符、`IsNot` 运算符和 `Like` 运算符具有特定的比较功能，它们与上表中的运算符不同。  
  
## 比较数字  
 当 `Single` 类型的表达式与 `Double` 类型的表达式比较时，`Single` 表达式被转换为 `Double`。  此行为与 Visual Basic 6 中的行为相反。  
  
 同样，当 `Decimal` 类型的表达式与 `Single` 或 `Double` 类型的表达式比较时，`Decimal` 表达式被转换为 `Single` 或 `Double`。  对于 `Decimal` 表达式，任何小于 1E\-28 的小数值都将丢失。  这种丢失小数值的情况可能导致比较两个并不相等的值时却得到相等的结果。  因此，在使用相等运算符 \(`=`\) 比较两个浮点变量时应多加小心。  更好的方法是测试一下两个数之差的绝对值是否小于一个小的可接受公差。  
  
### 浮点不精确  
 使用浮点数字时，请记住它们在内存中不一定有精确的表示形式。  对于某些操作（例如值比较和 [Mod 运算符](../../../visual-basic/language-reference/operators/mod-operator.md)），这可能导致意外的结果。  有关更多信息，请参见 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)。  
  
## 比较字符串  
 当比较字符串时，字符串表达式根据字符串的字母排序顺序进行计算，排序顺序取决于 `Option Compare` 设置。  
  
 `Option Compare Binary` 基于从字符的内部二进制表示形式导出的排序顺序进行字符串比较。  排序顺序取决于代码页。  下面的示例演示了典型的二进制排序顺序。  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 `Option Compare Text` 基于由应用程序的区域设置确定的不区分大小写的文本排序顺序进行字符串比较。  在上述示例中设置 `Option Compare Text` 并对字符进行排序时，将应用下面的文本排序顺序：  
  
 `(A=a) < (À= à) < (B=b) < (E=e) < (Ê= ê) < (Ø = ø) < (Z=z)`  
  
### 区域设置相关性  
 当设置 `Option Compare Text` 时，字符串比较的结果可能取决于运行应用程序的区域设置。  两个字符在一个区域设置中的比较结果可能为相等，但在另一个区域设置中可能不相等。  如果要使用字符串比较作出重要决定，例如是否接受登录尝试，则应该对区域设置敏感度非常小心。  可以设置 `Option Compare Binary` 或调用 <xref:Microsoft.VisualBasic.Strings.StrComp%2A>，从而考虑区域设置。  
  
## 使用关系比较运算符的无类型编程  
 在 `Option Strict On` 情况下，不允许在 `Object` 表达式中使用关系比较运算符。  当 `Option Strict` 为 `Off`，且 `expression1` 或 `expression2` 为 `Object` 表达式时，运行时类型将确定比较它们的方式。  下表显示如何根据操作数的运行时类型比较表达式以及比较的结果。  
  
|操作数|比较方式|  
|---------|----------|  
|都为 `String`|根据字符串排序特征进行排序比较。|  
|都为数值|对象转换为 `Double` 类型，进行数值比较。|  
|一个是数值而另一个是 `String`|`String` 被转换为 `Double` 并执行数值比较。  如果 `String` 不能转换为 `Double`，将引发 <xref:System.InvalidCastException>。|  
|有一个或两个都是 `String` 以外的引用类型|引发 <xref:System.InvalidCastException> 异常。|  
  
 数值比较将 `Nothing` 视为 0。  字符串比较将 `Nothing` 视为 `""`（空字符串）。  
  
## 重载  
 关系比较运算符（`<`、  `<=`、`>`、`>=`、`=`、`<>`）可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用任何这些运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
 请注意，[\= 运算符](../../../visual-basic/language-reference/operators/assignment-operator.md) 只能重载为关系比较运算符，而不能重载为赋值运算符。  
  
## 示例  
 下面的示例演示用来比较表达式的关系比较运算符的各种用法。  关系比较运算符返回 `Boolean` 结果，此结果表示所声明的表达式的计算结果是否为 `True`。  当您将 `>` 和 `<` 运算符应用于字符串时，将按照字符串的正常字母排序顺序进行比较。  此顺序取决于区域设置。  排序是否区分大小写取决于 [Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md) 设置。  
  
 [!code-vb[VbVbalrOperators#1](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/comparison-operators_1.vb)]  
  
 在上面的示例中，第一次比较返回 `False`，其余的比较返回 `True`。  
  
## 请参阅  
 <xref:System.InvalidCastException>   
 [\= 运算符](../../../visual-basic/language-reference/operators/assignment-operator.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [比较运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)