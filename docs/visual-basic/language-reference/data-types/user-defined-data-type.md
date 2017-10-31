---
title: "用户定义的数据类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "UserDefined"
  - "UDT"
  - "vb.UDT"
  - "User-Defined"
  - "vb.UserDefined"
  - "vb.User-Defined"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据类型 [Visual Basic], 分配"
  - "数据类型 [Visual Basic], 用户定义的"
  - "Structure 语句"
  - "结构, 作为用户定义的数据类型"
  - "类型 [Visual Basic], 用户定义的"
  - "用户定义的数据类型"
  - "用户定义的数据类型, 结构声明"
  - "用户定义的数据类型, Visual Basic 中的结构"
  - "用户定义的数据类型, Visual Basic"
  - "用户定义的类型"
  - "用户定义的类型, 结构声明"
  - "用户定义的类型, Visual Basic 中的结构"
  - "用户定义的类型, Visual Basic"
ms.assetid: be913dca-a364-4a51-96a1-549a1b390b0a
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 用户定义的数据类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

以您定义的格式保存数据。  `Structure` 语句将定义此格式。  
  
 Visual Basic 的以前版本支持用户定义的类型 \(UDT\)。  当前版本则将用户定义的类型扩展为结构。  结构是一个或多个不同数据类型的成员的串联。  Visual Basic 将一个结构视为一个单元，尽管如此，您仍然可以单独访问其成员。  
  
## 备注  
 当您需要将不同的数据类型组合为一个单元时，或者当所有基本数据类型都无法满足您的需求时，可以定义和使用结构数据类型。  
  
 结构数据类型的默认值由它的每个成员的默认值组合而成。  
  
## 声明格式  
 结构声明以 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md) 开始，以 `End` `Structure` 语句结束。  `Structure` 语句提供结构的名称，即结构所定义的数据类型的标识符。  代码中的其他部分可以使用此标识符声明变量、参数以及函数返回值（其数据类型为此结构的数据类型）。  
  
 `Structure` 和 `End` `Structure` 语句之间的声明定义结构的成员。  
  
## 成员访问级别  
 您必须使用 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md) 或一个指定访问级别的语句（如 [Public](../../../visual-basic/language-reference/modifiers/public.md)、[Friend](../../../visual-basic/language-reference/modifiers/friend.md) 或 [Private](../../../visual-basic/language-reference/modifiers/private.md)）声明每个成员。  如果使用 `Dim` 语句，则访问级别默认为 Public。  
  
## 编程提示  
  
-   **内存消耗。**与所有的复合数据类型一样，您无法通过将结构成员的名义存储分配相加来得到确切的总内存消耗。  此外，不能完全假定成员在内存中的存储顺序与声明的顺序相同。  如果需要控制结构的存储布局，可以对 `Structure` 语句应用 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 特性。  
  
-   **互操作注意事项。**如果您使用的组件不是为 .NET Framework 编写的组件（如自动化对象或 COM 对象），请记住，其他环境中的用户定义类型与 Visual Basic 结构类型不兼容。  
  
-   **扩大。**其他数据类型与任何结构数据类型之间不会进行任何自动转换。  您可以使用 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md) 在结构中定义转换运算符，也可以将每个转换运算符声明为 `Widening` 或 `Narrowing`。  
  
-   **类型字符。**结构数据类型没有文本类型字符或标识符类型字符。  
  
-   **Framework 类型。**.NET Framework 中没有相应的类型。  所有结构均继承自 .NET Framework 的 <xref:System.ValueType?displayProperty=fullName> 类，但是没有哪个结构与 <xref:System.ValueType?displayProperty=fullName> 相对应。  
  
## 示例  
 下面的示例演示结构声明的大致形式。  
  
```  
[Public | Protected | Friend | Protected Friend | Private] Structure structname  
    {Dim | Public | Friend | Private} member1 As datatype1  
    ' ...  
    {Dim | Public | Friend | Private} memberN As datatypeN  
End Structure  
```  
  
## 请参阅  
 <xref:System.ValueType>   
 <xref:System.Runtime.InteropServices.StructLayoutAttribute>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Widening](../../../visual-basic/language-reference/modifiers/widening.md)   
 [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)