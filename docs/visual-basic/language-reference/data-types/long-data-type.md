---
title: "Long 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Long"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "& 标识符类型字符"
  - "数据类型 [Visual Basic], 分配"
  - "数据类型 [Visual Basic], 整数"
  - "标识符类型字符串, &"
  - "整数数字"
  - "整数, 数据类型"
  - "整数, 类型"
  - "整数数据类型"
  - "L 文本类型字符"
  - "文本类型的字符, L"
  - "Long 数据类型"
  - "Long 关键字"
  - "数字, integer"
  - "数字, 整个"
  - "整数"
ms.assetid: b4770c34-1804-4f8c-b512-c10b0893e516
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Long 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存 64 位（8 字节）有符号整数，值的范围为 \-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 \(9.2...E\+18\)。  
  
## 备注  
 使用 `Long` 数据类型保存位数太多以至不适合 `Integer` 数据类型的整数数字。  
  
 `Long` 的默认值为 0。  
  
## 编程提示  
  
-   **互操作注意事项。**如果您使用的不是为 .NET Framework 编写的组件（如自动化或 COM 对象），请记住在其他环境中，`Long` 具有不同的数据长度（32 位）。  若将一个 32 位参数传递给这样的组件，在新的 Visual Basic 代码中应将其声明为 `Integer` 而不是 `Long`。  
  
     此外，自动化在 Windows 95、Windows 98、Windows ME 或 Windows 2000 上不支持 64 位整数。  不能将 Visual Basic `Long` 参数传递给这些操作系统上的自动化组件。  
  
-   **扩大。** `Long` 数据类型扩大为 `Decimal`、`Single` 或 `Double`。  这意味着您可以将 `Long` 转换为这些类型中的任一类型，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **类型字符。**将文本类型字符 `L` 追加到文本会将其强制转换成 `Long` 数据类型。  将标识符类型字符 `&` 追加到任何标识符会将其强制转换成 `Long`。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.Int64?displayProperty=fullName> 结构。  
  
## 请参阅  
 <xref:System.Int64>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Integer 数据类型](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [Short 数据类型](../../../visual-basic/language-reference/data-types/short-data-type.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)