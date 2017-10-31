---
title: "返回 CStr 函数的值 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "CStr 函数"
  - "日期数据类型, 转换"
  - "日期 [Visual Basic]"
  - "日期 [Visual Basic], CStr 函数返回值"
  - "String 数据类型, 转换"
  - "字符串 [Visual Basic], 返回值"
  - "时间, CStr 函数返回值"
  - "类型转换"
ms.assetid: 3aa744e7-1419-45d5-85e3-e5abc2953673
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 返回 CStr 函数的值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

下表说明 `CStr` 针对不同的 `expression` 数据类型所返回的值。  
  
|如果 `expression` 类型为|`CStr` 返回|  
|-------------------------|---------------|  
|[Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|包含“True”或“False”的字符串。|  
|[日期数据类型](../../../visual-basic/language-reference/data-types/date-data-type.md)|以系统的短日期格式包含 `Date` 值（日期和时间）的字符串。|  
|[数值型数据类型](../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)|表示数字的字符串。|  
  
## CStr 和 Date  
 `Date` 类型始终包含日期和时间信息。  为进行类型转换，Visual Basic 将 1\/1\/0001（公元 1 年 1 月 1 日）作为日期的“中性值”，将 00:00:00（午夜）作为时间的中性值。  `CStr` 将不在结果字符串中包含中性值。  例如，如果将 `#January 1, 0001 9:30:00#` 转换为字符串，结果为“9:30:00 AM”；日期信息被删除了。  但是，日期信息仍然在原来的 `Date` 值中提供，并可以使用 <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> 等函数恢复。  
  
> [!NOTE]
>  `CStr` 函数根据应用程序的当前区域设置执行转换。  若要获得特定区域中数字的字符串表示形式，请使用数字的 `ToString(IFormatProvider)` 方法。  例如，将类型 `Double` 的值转换为 `String` 时，请使用 <xref:System.Double.ToString%2A?displayProperty=fullName>。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A>   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md)   
 [日期数据类型](../../../visual-basic/language-reference/data-types/date-data-type.md)