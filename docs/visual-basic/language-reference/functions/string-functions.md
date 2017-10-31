---
title: "字符串函数 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "字符串函数"
ms.assetid: f1bf9ac2-cbcf-4298-ae51-53182076bdc8
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 字符串函数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

下表列出了 Visual Basic 提供的用于搜索和操作字符串的函数。  
  
|.NET Framework 方法|描述|  
|-----------------------|--------|  
|<xref:Microsoft.VisualBasic.Strings.Asc%2A>, <xref:Microsoft.VisualBasic.Strings.AscW%2A>|返回一个 `Integer` 值，该值表示与某个字符相对应的字符代码。|  
|<xref:Microsoft.VisualBasic.Strings.Chr%2A>, <xref:Microsoft.VisualBasic.Strings.ChrW%2A>|返回与指定字符代码相关联的字符。|  
|<xref:Microsoft.VisualBasic.Strings.Filter%2A>|返回一个从零开始的数组，该数组包含基于指定筛选条件的 `String` 数组的子集。|  
|<xref:Microsoft.VisualBasic.Strings.Format%2A>|返回根据格式 `String` 表达式中包含的指令设置格式的字符串。|  
|<xref:Microsoft.VisualBasic.Strings.FormatCurrency%2A>|返回一个格式为货币值的表达式，该货币值使用系统控制面板中定义的货币符号。|  
|<xref:Microsoft.VisualBasic.Strings.FormatDateTime%2A>|返回一个表示日期\/时间值的字符串表达式。|  
|<xref:Microsoft.VisualBasic.Strings.FormatNumber%2A>|返回格式化为数字的表达式。|  
|<xref:Microsoft.VisualBasic.Strings.FormatPercent%2A>|返回格式化为带后缀 % 字符的百分数（即乘以 100）的表达式。|  
|<xref:Microsoft.VisualBasic.Strings.InStr%2A>|返回一个整数，该整数指定一个字符串在另一个字符串中的第一个匹配项的起始位置。|  
|<xref:Microsoft.VisualBasic.Strings.InStrRev%2A>|返回某一字符串从另一字符串的右侧开始算起第一次出现的位置。|  
|<xref:Microsoft.VisualBasic.Strings.Join%2A>|返回通过连接一个数组中包含的若干子字符串创建的字符串。|  
|<xref:Microsoft.VisualBasic.Strings.LCase%2A>|返回将转换为小写的字符串或字符。|  
|<xref:Microsoft.VisualBasic.Strings.Left%2A>|返回一个字符串，该字符串包含从某字符串左侧算起的指定数量的字符。|  
|<xref:Microsoft.VisualBasic.Strings.Len%2A>|返回一个整数，该整数包含某字符串中的字符数。|  
|<xref:Microsoft.VisualBasic.Strings.LSet%2A>|返回一个左对齐字符串，该字符串包含调整为指定长度的指定的字符串。|  
|<xref:Microsoft.VisualBasic.Strings.LTrim%2A>|返回一个字符串，该字符串包含指定字符串的没有前导空格的副本。|  
|<xref:Microsoft.VisualBasic.Strings.Mid%2A>|从一个字符串返回包含指定数量字符的字符串。|  
|<xref:Microsoft.VisualBasic.Strings.Replace%2A>|返回一个字符串，其中的指定子字符串已由另一个子字符串替换了指定的次数。|  
|<xref:Microsoft.VisualBasic.Strings.Right%2A>|返回一个字符串，其中包含从某个字符串右端开始的指定数量的字符。|  
|<xref:Microsoft.VisualBasic.Strings.RSet%2A>|返回包含调整为指定长度的指定字符串的右对齐字符串。|  
|<xref:Microsoft.VisualBasic.Strings.RTrim%2A>|返回一个字符串，该字符串包含指定字符串的没有尾随空格的副本。|  
|<xref:Microsoft.VisualBasic.Strings.Space%2A>|返回由指定数量空格组成的字符串。|  
|<xref:Microsoft.VisualBasic.Strings.Split%2A>|返回一个从零开始的一维数组，其中包含指定数量的子字符串。|  
|<xref:Microsoft.VisualBasic.Strings.StrComp%2A>|根据字符串的比较结果返回 \-1、0 或 1。|  
|<xref:Microsoft.VisualBasic.Strings.StrConv%2A>|返回按照指定方式转换的字符串。|  
|<xref:Microsoft.VisualBasic.Strings.StrDup%2A>|返回由指定字符重复指定次数后形成的字符串或对象。|  
|<xref:Microsoft.VisualBasic.Strings.StrReverse%2A>|返回指定字符串的字符顺序是相反的字符串。|  
|<xref:Microsoft.VisualBasic.Strings.Trim%2A>|返回一个字符串，该字符串包含指定字符串的没有前导和尾随空格的副本。|  
|<xref:Microsoft.VisualBasic.Strings.UCase%2A>|返回一个字符串或字符，其中包含转换为大写的指定字符串。|  
  
 可以使用 [Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md) 语句设置是按照由系统区域设置决定的不区分大小写的文本排序顺序 \(`Text`\) 对字符串进行比较，还是按照字符的内部二进制表示形式 \(`Binary`\) 进行比较。  默认文本比较方法为 `Binary`。  
  
## 示例  
 本例使用 `UCase` 函数返回字符串的大写版本。  
  
 [!code-vb[VbVbalrStrings#31](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_1.vb)]  
  
## 示例  
 此示例使用 `LTrim` 函数去除字符串变量的前导空格，使用 `RTrim` 函数去除尾随空格，  并使用 `Trim` 函数同时去除这两种类型的空格。  
  
 [!code-vb[VbVbalrStrings#25](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_2.vb)]  
  
## 示例  
 本例使用 `Mid` 函数从字符串返回指定数量的字符。  
  
 [!code-vb[VbVbalrStrings#17](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_3.vb)]  
  
## 示例  
 本例使用 `Len` 返回字符串中的字符数。  
  
 [!code-vb[VbVbalrStrings#33](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_4.vb)]  
  
## 示例  
 本例使用 `InStr` 函数返回一个字符串在另一个字符串中的第一个匹配项的位置。  
  
 [!code-vb[VbVbalrStrings#8](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_5.vb)]  
  
## 示例  
 此示例演示同时使用 `String` 格式和用户定义格式格式化值的 `Format` 函数的各种用法。  对于日期分隔符 \(`/`\)、时间分隔符 \(`:`\) 和 AM\/PM 指示符（`t` 和 `tt`），系统显示的实际格式化输出取决于代码使用的区域设置。  当在开发环境中显示时间和日期时，使用代码区域设置的短时间格式和短日期格式。  
  
> [!NOTE]
>  对于使用 24 小时制的区域设置，AM\/PM 指示符（`t` 和 `tt`）不显示任何内容。  
  
 [!code-vb[VbVbalrStrings#27](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_6.vb)]  
  
## 请参阅  
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [Visual Basic 运行库成员](../../../visual-basic/language-reference/runtime-library-members.md)   
 [字符串操作摘要](../../../visual-basic/language-reference/keywords/string-manipulation-summary.md)