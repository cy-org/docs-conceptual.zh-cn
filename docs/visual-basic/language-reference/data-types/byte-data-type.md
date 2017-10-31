---
title: "Byte 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Byte"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Byte 数据类型"
  - "数据类型 [Visual Basic], 分配"
ms.assetid: eed44dff-eaee-4937-a89f-444e418e74f6
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Byte 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存 8 位（1 字节）无符号整数，值的范围为 0 到 255。  
  
## 备注  
 用 `Byte` 数据类型包含二进制数据。  
  
 `Byte` 的默认值为 0。  
  
## 编程提示  
  
-   **负数。**因为 `Byte` 是无符号类型，所以不能表示负数。  如果对计算结果为类型 `Byte` 的表达式使用一元负 \(`-`\) 运算符，则 Visual Basic 首先将该表达式转换为 `Short`。  
  
-   **格式转换。**当 Visual Basic 读取或写入文件或调用 DLL、方法和属性时，它可以自动转换数据格式。  存储在 `Byte` 变量和数组中的二进制数据在格式转换中被保留。  不应对二进制数据使用 `String` 变量，因为在 ANSI 和 Unicode 格式之间转换时其内容会损坏。  
  
-   **扩大。** `Byte` 数据类型扩大为 `Short`、`UShort`、`Integer`、`UInteger`、`Long`、`ULong`、`Decimal`、`Single` 或 `Double`。  这意味着您可以将 `Byte` 转换为这些类型中的任何一种，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **类型字符。** `Byte` 不包含文本类型字符或标识符类型字符。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.Byte?displayProperty=fullName> 结构。  
  
## 示例  
 在下面的示例中，`b` 是一个 `Byte` 变量。  各语句演示变量的范围和对其应用移位运算符。  
  
 [!code-vb[VbVbalrDataTypes#16](../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/byte-data-type_1.vb)]  
  
## 请参阅  
 <xref:System.Byte?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)