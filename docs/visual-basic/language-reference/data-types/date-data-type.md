---
title: "Date 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Date"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Date 文本的 # 说明符"
  - "数据类型 [Visual Basic], 分配"
  - "数据值"
  - "日期数据类型"
  - "Date 文本"
  - "日期, 日期数据类型"
  - "日期, Visual Basic 数据类型"
  - "文本, 日期"
  - "时间, 日期数据类型"
  - "时间, Visual Basic 数据类型"
ms.assetid: d9edf5b0-e85e-438b-a1cf-1f321e7c831b
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Date 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存 IEEE 64 位（8 字节）值，它代表从 0001 年 1 月 1 日到 9999 年 12 月 31 日的日期，12:00:00 AM（午夜）到 11:59:59.9999999 PM 的时间。  每个增量表示自公历 1 年 1 月 1 日开始后经过的 100 纳秒的时间。  最大值表示 10000 年 1 月 1 日开始之前的 100 纳秒。  
  
## 备注  
 使用 `Date` 数据类型包含日期值、时间值或日期和时间值。  
  
 `Date` 的默认值为 0001 年 1 月 1 日 0:00:00（午夜）。  
  
 可以从 <xref:Microsoft.VisualBasic.DateAndTime> 类获取当前日期和时间。  
  
## 格式要求  
 必须将 `Date` 文字括在数字符号 \(`# #`\) 内。  必须以 M\/d\/yyyy 格式（例如 `#5/31/1993#`）或 yyyy\-MM\-dd 格式（例如 `#1993-5-31#`）指定日期值。  首先指定年份时，可以使用斜杠。  此要求与你所在的区域设置以及计算机的日期和时间格式设置相互独立。  
  
 此限制的原因是，代码的含义永远不会依据应用程序在其中运行的区域设置而改变。  假设硬编码 `Date` 文字 `#3/4/1998#` 意图使其表示 1998 年 3 月 4 日。  在使用 mm\/dd\/yyyy 的区域，3\/4\/1998 将按照你的意图进行编译。  但是，假设你在许多国家\/地区部署你的应用程序。  在使用 dd\/mm\/yyyy 的区域，硬编码的文本将编译为 1998 年 4 月 3 日。  在使用 yyyy\/mm\/dd 的区域，该文字将会无效（0003 年 4 月 1998 日）并导致编译器错误。  
  
## 问题解决  
 若要将 `Date` 文字转换为你所在区域的格式或自定义格式，请将该文字提供给 <xref:Microsoft.VisualBasic.Strings.Format%2A> 函数，并指定预定义的或用户定义的日期格式。  下面的示例演示这一操作。  
  
```  
MsgBox("The formatted date is " & Format(#5/31/1993#, "dddd, d MMM yyyy"))  
```  
  
 或者，可以使用 <xref:System.DateTime> 结构的重载构造函数之一来组合日期和时间值。  以下示例创建一个表示 1993 年 3 月 31 日下午 12:14 的值。  
  
```  
Dim dateInMay As New System.DateTime(1993, 5, 31, 12, 14, 0)   
```  
  
## 小时格式  
 可以 12 小时制或 24 小时制格式指定时间值，例如 `#1:15:30 PM#` 或 `#13:15:30#`。  但是，如果未指定分钟或秒，则必须指定 AM 或 PM。  
  
## 日期和时间默认值  
 如果不在日期\/时间文字中包括日期，则 Visual Basic 会将值的日期部分设置为 0001 年 1 月 1 日。  如果不在日期\/时间文字中包括时间，则 Visual Basic 会将值的时间部分设置为一天的开始，即午夜 \(0:00:00\)。  
  
## 类型转换  
 如果将 `Date` 值转换为 `String` 类型，则 Visual Basic 根据由运行时区域设置指定的短日期格式呈现日期，根据运行时区域设置指定的时间格式（12 小时制或 24 小时制）呈现时间。  
  
## 编程提示  
  
-   **互操作注意事项。** 如果你与不是为 .NET Framework 编写的组件（如自动化或 COM 对象）交互，请记住，其他环境中的日期\/时间类型与 Visual Basic `Date` 类型不兼容。  如果将日期\/时间参数传递给此类组件，请在新的 Visual Basic 代码中将其声明为 `Double` 而不是 `Date`，并使用转换方法 <xref:System.DateTime.FromOADate%2A?displayProperty=fullName> 和 <xref:System.DateTime.ToOADate%2A?displayProperty=fullName>。  
  
-   **类型字符。** `Date` 没有文本类型字符或标识符类型字符。  但是，编译器会将括在数字符号 \(`# #`\) 内的文本作为 `Date`。  
  
-   **Framework 类型。** .NET Framework 中的对应类型是 <xref:System.DateTime?displayProperty=fullName> 结构。  
  
## 示例  
 `Date` 数据类型的变量或常数都包含日期和时间。  下面的示例阐释了这一点。  
  
```  
Dim someDateAndTime As Date = #8/13/2002 12:14 PM#  
```  
  
## 请参阅  
 <xref:System.DateTime?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [标准日期和时间格式字符串](../Topic/Standard%20Date%20and%20Time%20Format%20Strings.md)   
 [自定义日期和时间格式字符串](../Topic/Custom%20Date%20and%20Time%20Format%20Strings.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)