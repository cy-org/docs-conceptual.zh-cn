---
title: "Like 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Like"
  - "vb.Like"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "? 符号, 通配符"
  - "比较运算符"
  - "数据 [Visual Basic], 排序"
  - "数据 [Visual Basic], 字符串比较"
  - "Like 运算符 [Visual Basic]"
  - "运算符 [Visual Basic], 模式匹配"
  - "模式匹配"
  - "类似于"
  - "字符串比较 [Visual Basic], Like 运算符"
  - "字符串比较 [Visual Basic], Like 运算符"
  - "字符串比较 [Visual Basic], 对数据进行排序"
  - "字符串 [Visual Basic], 比较"
  - "字符串 [Visual Basic], 匹配"
  - "symbols, 通配符"
  - "文本 [Visual Basic], 比较"
  - "通配符, Like 运算符"
ms.assetid: 966283ec-80e2-4294-baa8-c75baff804f9
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Like 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

根据模式来比较字符串。  
  
## 语法  
  
```  
  
result = string Like pattern  
```  
  
## 部件  
 `result`  
 必选。  任何 `Boolean` 变量。  结果是 `Boolean` 值，它表示 `string` 是否满足 `pattern`。  
  
 `string`  
 必选。  任何 `String` 表达式。  
  
 `pattern`  
 必选。  任何符合“备注”中描述的模式匹配约定的 `String` 表达式。  
  
## 备注  
 如果 `string` 的值满足 `pattern` 中包含的模式，则 `result` 为 `True`。  如果字符串不满足该模式，则 `result` 为 `False`。  如果 `string` 和 `pattern` 都是空字符串，则结果为 `True`。  
  
## 比较方法  
 `Like` 运算符的行为取决于 [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)。  每个源文件的默认字符串比较方法是 `Option Compare Binary`。  
  
## 模式选项  
 内置的模式匹配为字符串比较提供了一种多功能工具。  模式匹配功能允许您将 `string` 中的每个字符与特定字符、通配符字符、字符列表或某个字符范围进行匹配。  下表显示 `pattern` 中允许的字符和这些字符的匹配项。  
  
|`pattern` 中的字符|`string` 中的匹配项|  
|--------------------|--------------------|  
|`?`|任何单个字符|  
|`*`|零或更多字符|  
|`#`|任何单个数字（0 到 9）|  
|`[` `charlist` `]`|`charlist` 中的任何单个字符|  
|`[!` `charlist` `]`|不在 `charlist` 中的任何单个字符|  
  
## 字符列表  
 括在方括号 \(`[ ]`\) 内的一个或多个字符的组 \(`charlist`\) 可以用于匹配 `string` 中的任何单个字符，并且可以包含几乎任何字符代码（包括数字）。  
  
 `charlist` 开始处的感叹号 \(`!`\) 意味着仅当在 `string` 中找到除 `charlist` 以外的任何字符时才发生匹配。  当在方括号外使用时，感叹号匹配它自己。  
  
## 特殊字符  
 若要与左方括号 \(`[`\)、问号 \(`?`\)、数字号 \(`#`\) 和星号 \(`*`\) 这些特殊字符匹配，必须用方括号将它们括起。  右方括号 \(`]`\) 不能在组中用来与自身匹配，但它可用在组外作为单个字符。  
  
 可以将字符序列 `[]` 视为零长度字符串 \(`""`\)；  但不能将其作为括在括号中的字符列表的一部分。  如果要检查 `string` 中的某个位置是包含一组字符还是不包含任何字符，可以使用两次 `Like`。  有关示例，请参见[如何：将字符串与模式相匹配](../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md)。  
  
## 字符范围  
 通过使用连字符 \(`–`\) 将范围的上下限分开，`charlist` 可以指定字符的范围。  例如，如果 `string` 中的相应字符位置包含范围 `A` 至 `Z` 中的任何字符，则 `[A–Z]` 将引起匹配；如果相应的字符位置包含范围 `H` 至 `L` 之外的任何字符，则 `[!H–L]` 将引起匹配。  
  
 在指定字符范围时，这些字符必须以升序排序顺序出现（即，从最低到最高）。  因此，`[A–Z]` 是有效的模式，但 `[Z–A]` 不是。  
  
### 多字符范围  
 若要为同一个字符位置指定多个范围，请将这些范围放在没有分隔符的同一对括号中。  例如，如果 `string` 中的相应字符位置包含范围 `A` 至 `C` 或范围 `X` 至 `Z` 中的任何字符，则 `[A–CX–Z]` 将引起匹配。  
  
### 连字符的用法  
 连字符 \(`–`\) 可以出现在 `charlist` 的开始处（如果有感叹号，则在它后面）或结尾处以匹配它自己。  在任何其他位置，连字符标识由连字符两侧的字符界定的字符范围。  
  
## 排序序列  
 指定的范围的含义取决于在运行时的字符排序（由 `Option` `Compare` 和运行代码的系统的区域设置确定）。  对于 `Option``Compare``Binary`，范围 `[A–E]` 与 `A`、`B`、`C`、`D` 和 `E` 匹配；  对于 `Option``Compare``Text`，`[A–E]` 与 `A`、`a`、`À`、`à`、`B`、`b`、`C`、`c`、`D`、`d`、`E` 和 `e` 匹配。  该范围与 `Ê` 或 `ê` 不匹配，因为按照排序顺序，重音字符在非重音字符之后。  
  
## 二合字母字符  
 在某些语言中，有一些表示两种不同字符的字母字符。  例如，有几种语言使用字符 `æ` 来表示字符 `a` 和 `e`（当这两个字符一起出现时）。  `Like` 运算符认为该单个二合字母字符与这两个单独的字符是等效的。  
  
 当在系统区域设置中指定使用二合字母字符的语言时，在 `pattern` 或 `string` 中出现的单个二合字母字符都匹配其他字符串中等效的双字符序列。  与此类似，括在方括号内的 `pattern` 中的单个二合字母字符（独立存在、在列表中或在某个范围内）匹配 `string` 中等效的双字符序列。  
  
## 重载  
 `Like` 运算符可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 本示例使用 `Like` 运算符将字符串与各种模式比较。  结果变为 `Boolean` 变量，它表示每个字符串是否满足该模式。  
  
 [!code-vb[VbVbalrOperators#30](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/like-operator_1.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Strings.InStr%2A>   
 <xref:Microsoft.VisualBasic.Strings.StrComp%2A>   
 [比较运算符](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [如何：将字符串与模式相匹配](../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md)