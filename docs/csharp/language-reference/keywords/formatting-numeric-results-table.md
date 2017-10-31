---
title: "设置数值结果表的格式（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- formatting [C#]
- numeric formatting [C#]
- String.Format method
- Console.Write method
ms.assetid: 120ba537-4448-4c62-8676-7a8fdd98f496
caps.latest.revision: 14
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 16976f5a59bd4eb0eca29553aff87d4fe0b1d247
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="formatting-numeric-results-table-c-reference"></a>设置数值结果表的格式（C# 参考）
可通过使用 <xref:System.String.Format%2A?displayProperty=fullName> 方法或 <xref:System.Console.Write%2A?displayProperty=fullName> 或 <xref:System.Console.WriteLine%2A?displayProperty=fullName> 方法（这两种方法调用 `String.Format`）来设置数值结果的格式。 通过使用格式字符串指定格式。 下表包含支持的标准格式字符串。 格式字符串采用以下形式：`Axx`，其中 `A` 是格式说明符，`xx` 是精度说明符。 格式说明符控制应用于数值的格式类型，而精度说明符则控制格式化输出的有效位数或小数位数。 精度说明符值的范围为 0 到 99。  
  
 有关标准格式字符串和自定义格式字符串的详细信息，请参阅[格式设置类型](../../../standard/base-types/formatting-types.md)。 有关 `String.Format` 方法的更多信息，请参见 <xref:System.String.Format%2A?displayProperty=fullName>。  
  
|格式说明符|描述|示例|输出|  
|----------------------|-----------------|--------------|------------|  
|C 或 c|货币|Console.Write("{0:C}", 2.5);<br /><br /> Console.Write("{0:C}", -2.5);|$2.50<br /><br /> ($2.50)|  
|D 或 d|Decimal|Console.Write("{0:D5}", 25);|00025|  
|E 或 e|科学记数法|Console.Write("{0:E}", 250000);|2.500000E+005|  
|F 或 f|定点|Console.Write("{0:F2}", 25);<br /><br /> Console.Write("{0:F0}", 25);|25.00<br /><br /> 25|  
|G 或 g|常规|Console.Write("{0:G}", 2.5);|2.5|  
|N 或 n|数字|Console.Write("{0:N}", 2500000);|2,500,000.00|  
|X 或 x|十六进制|Console.Write("{0:X}", 250);<br /><br /> Console.Write("{0:X}", 0xffff);|FA<br /><br /> FFFF|  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [标准数字格式字符串](../../../standard/base-types/standard-numeric-format-strings.md)   
 [类型参考表](../../../csharp/language-reference/keywords/reference-tables-for-types.md)   
 [字符串](../../../csharp/language-reference/keywords/string.md)

