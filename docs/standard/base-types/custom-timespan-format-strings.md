---
title: "自定义的 TimeSpan 格式字符串 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "自定义时间间隔格式字符串"
  - "自定义 TimeSpan 格式字符串"
  - "格式说明符, 自定义时间间隔"
  - "格式字符串"
  - "格式设置 [.NET Framework], 时间"
  - "格式设置 [.NET Framework], 时间间隔"
ms.assetid: a63ebf55-7269-416b-b4f5-286f6c03bf0e
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# 自定义的 TimeSpan 格式字符串
<xref:System.TimeSpan> 格式字符串定义由格式设置操作生成的 <xref:System.TimeSpan> 值的字符串表示形式。  一个自定义格式字符串包含一个或多个自定义 <xref:System.TimeSpan> 格式说明符与任意数量的文本字符。  任何非[标准 TimeSpan 格式字符串](../../../docs/standard/base-types/standard-timespan-format-strings.md)的字符串被解释为自定义 <xref:System.TimeSpan> 格式字符串。  
  
> [!IMPORTANT]
>  自定义 <xref:System.TimeSpan> 格式说明符不包含占位符分隔符，如用于分隔天与小时的符号、用于分隔小时与分钟的符号或用于分隔秒与秒的小数部分的符号。  相反，这些符号必须作为字符串文本包含在自定义格式字符串中。  例如，`"dd\.hh\:mm"` 将句点 \(.\) 定义为日期与小时之间的分隔符，并将冒号 \(:\) 定义为小时与分钟之间的分隔符。  
>   
>  自定义<xref:System.TimeSpan>格式说明符还包括使您能够区分正和负时间间隔之间的某个信号符号。  若要包含符号符号，必须使用条件逻辑构造格式字符串。  [其他字符](#Other)部分包括一个示例。  
  
 <xref:System.TimeSpan> 值的字符串表示形式由对 <xref:System.TimeSpan.ToString%2A?displayProperty=fullName> 方法重载的调用和支持复合格式设置（如 <xref:System.String.Format%2A?displayProperty=fullName>）的方法生成。  有关更多信息，请参见[格式化类型](../../../docs/standard/base-types/formatting-types.md)和[复合格式设置](../../../docs/standard/base-types/composite-formatting.md)。  下面的示例演示自定义格式字符串在格式设置操作中的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customformatexample1.cs#1)]
 [!code-vb[Conceptual.TimeSpan.Custom#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customformatexample1.vb#1)]  
  
 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName>和<xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName>方法还可使用自定义 <xref:System.TimeSpan>格式字符串来定义分析操作所需的输入字符串格式。（分析操作会将值的字符串表示形式转换为该值。）下面的示例演示标准格式字符串在分析操作中的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customparseexample1.cs#2)]
 [!code-vb[Conceptual.TimeSpan.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customparseexample1.vb#2)]  
  
<a name="table"></a> 下表描述了自定义日期和时间格式说明符。  
  
|格式说明符|描述|示例|  
|-----------|--------|--------|  
|“d”、“%d”|时间间隔中的整天数。<br /><br /> 有关更多信息，请参见[“d”自定义格式说明符](#dSpecifier)。|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%d`\> "6"<br /><br /> `d\.hh\:mm` \-\-\> "6.14:32"|  
|“dd”\-“dddddddd”|时间间隔中的整天数，可以根据需要用前导零填充该数字。<br /><br /> 有关更多信息，请参见[“dd”\-“dddddddd”自定义格式说明符](#ddSpecifier)。|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `ddd` \> "006"<br /><br /> `dd\.hh\:mm` \-\> "06.14:32"|  
|“h”、“%h”|时间间隔中未计入天部分中的整小时数。  一位数的小时数没有前导零。<br /><br /> 有关更多信息，请参见[“h”自定义格式说明符](#hSpecifier)。|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%h` \> "14"<br /><br /> `hh\:mm` \-\> "14:32"|  
|“hh”|时间间隔中未计入天部分中的整小时数。  一位数的小时数有一个前导零。<br /><br /> 有关更多信息，请参见[“hh”自定义格式说明符](#hhSpecifier)。|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `hh` \> "14"<br /><br /> `new TimeSpan(6, 8, 32, 17, 685):`<br /><br /> `hh` \-\-\> 08|  
|“m”、“%m”|时间间隔中未计入小时或天部分的整分钟数。  一位数的分钟数没有前导零。<br /><br /> 有关更多信息，请参见[“m”自定义格式说明符](#mSpecifier)。|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `%m` \-\> "8"<br /><br /> `h\:m` \-\> "14:8"|  
|“mm”|时间间隔中未计入小时或天部分的整分钟数。  一位数的分钟数有一个前导零。<br /><br /> 有关更多信息，请参见[“mm”自定义格式说明符](#mmSpecifier)。|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `mm` \> "08"<br /><br /> `new TimeSpan(6, 8, 5, 17, 685):`<br /><br /> `d\.hh\:mm\:ss` \-\-\> 6.08:05:17|  
|“s”、“%s”|时间间隔中未计入小时、天或分钟部分的整秒数。  一位数的秒数没有前导零。<br /><br /> 有关更多信息，请参见[“s”自定义格式说明符](#sSpecifier)。|`TimeSpan.FromSeconds(12.965)`:<br /><br /> `%s` \-\-\> 12<br /><br /> `s\.fff` \-\-\> 12.965|  
|“ss”|时间间隔中未计入小时、天或分钟部分的整秒数。一位数的秒数有一个前导零。<br /><br /> 有关更多信息，请参见[“ss”自定义格式说明符](#ssSpecifier)。|`TimeSpan.FromSeconds(6.965)`:<br /><br /> `ss` \-\-\> 06<br /><br /> `ss\.fff` \-\-\> 06.965|  
|“f”、“%f”|时间间隔中的十分之几秒。<br /><br /> 有关更多信息，请参见[“f”自定义格式说明符](#fSpecifier)。|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `f` \-\-\> 8<br /><br /> `ss\.f` \-\-\> 06.8|  
|“ff”|时间间隔中的百分之几秒。<br /><br /> 有关更多信息，请参见[“ff”自定义格式说明符](#ffSpecifier)。|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `ff` \-\-\> 89<br /><br /> `ss\.ff` \-\-\> 06.89|  
|“fff”|时间间隔中的毫秒。<br /><br /> 有关更多信息，请参见[“fff”自定义格式说明符](#f3Specifier)。|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `fff` \-\-\> 895<br /><br /> `ss\.fff` \-\-\> 06.895|  
|“ffff”|时间间隔中的万分之几秒。<br /><br /> 有关更多信息，请参见[“ffff”自定义格式说明符](#f4Specifier)。|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `ffff` \-\-\> 8954<br /><br /> `ss\.ffff` \-\-\> 06.8954|  
|“fffff”|时间间隔中的十万分之几秒。<br /><br /> 有关更多信息，请参见[“fffff”自定义格式说明符](#f5Specifier)。|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `fffff` \-\-\> 89543<br /><br /> `ss\.fffff` \-\-\> 06.89543|  
|“ffffff”|时间间隔中的百万分之几秒。<br /><br /> 有关更多信息，请参见[“ffffff”自定义格式说明符](#f6Specifier)。|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `ffffff` \-\-\> 895432<br /><br /> `ss\.ffffff` \-\-\> 06.895432|  
|“fffffff”|时间间隔中的千万分之几秒（或小数嘀嗒数）。<br /><br /> 有关更多信息，请参见[“fffffff”自定义格式说明符](#f7Specifier)。|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `fffffff` \-\-\> 8954321<br /><br /> `ss\.fffffff` \-\-\> 06.8954321|  
|“F”、“%F”|时间间隔中的十分之几秒。  如果该数字为零，则不显示任何内容。<br /><br /> 有关更多信息，请参见[“F”自定义格式说明符](#F_Specifier)。|`TimeSpan.Parse("00:00:06.32")`:<br /><br /> `%F`: 3<br /><br /> `TimeSpan.Parse("0:0:3.091")`:<br /><br /> `ss\.F`: 03.|  
|“FF”|时间间隔中的百分之几秒。  不包含任何小数尾随零或两个零位。<br /><br /> 有关更多信息，请参见[“FF”自定义格式说明符](#FF_Specifier)。|`TimeSpan.Parse("00:00:06.329")`:<br /><br /> `FF`: 32<br /><br /> `TimeSpan.Parse("0:0:3.101")`:<br /><br /> `ss\.FF`: 03.1|  
|“FFF”|时间间隔中的毫秒。  不包含任何小数尾随零。<br /><br /> 更多信息：|`TimeSpan.Parse("00:00:06.3291")`:<br /><br /> `FFF`: 329<br /><br /> `TimeSpan.Parse("0:0:3.1009")`:<br /><br /> `ss\.FFF`: 03.1|  
|“FFFF”|时间间隔中的万分之几秒。  不包含任何小数尾随零。<br /><br /> 有关更多信息，请参见[“FFFF”自定义格式说明符](#F4_Specifier)。|`TimeSpan.Parse("00:00:06.32917")`:<br /><br /> `FFFFF`: 3291<br /><br /> `TimeSpan.Parse("0:0:3.10009")`:<br /><br /> `ss\.FFFF`: 03.1|  
|“FFFFF”|时间间隔中的十万分之几秒。  不包含任何小数尾随零。<br /><br /> 有关更多信息，请参见[“FFFFF”自定义格式说明符](#F5_Specifier)。|`TimeSpan.Parse("00:00:06.329179")`:<br /><br /> `FFFFF`: 32917<br /><br /> `TimeSpan.Parse("0:0:3.100009")`:<br /><br /> `ss\.FFFFF`: 03.1|  
|“FFFFFF”|时间间隔中的百万分之几秒。  不显示任何小数尾随零。<br /><br /> 有关更多信息，请参见[“FFFFFF”自定义格式说明符](#F6_Specifier)。|`TimeSpan.Parse("00:00:06.3291791")`:<br /><br /> `FFFFFF`: 329179<br /><br /> `TimeSpan.Parse("0:0:3.1000009")`:<br /><br /> `ss\.FFFFFF`: 03.1|  
|“FFFFFFF”|时间间隔中的千万分之几秒。  不显示任何小数尾随零或七个零。<br /><br /> 有关更多信息，请参见[“FFFFFFF”自定义格式说明符](#F7_Specifier)。|`TimeSpan.Parse("00:00:06.3291791")`:<br /><br /> `FFFFFF`: 3291791<br /><br /> `TimeSpan.Parse("0:0:3.1900000")`:<br /><br /> `ss\.FFFFFF`: 03.19|  
|*'string*'|文本字符串分隔符。<br /><br /> 有关更多信息，请参见[其他字符](#Other)。|`new TimeSpan(14, 32, 17):`<br /><br /> `hh':'mm':'ss` \-\> "14:32:17"|  
|\\|转义字符。<br /><br /> 有关更多信息，请参见[其他字符](#Other)。|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` \-\> "14:32:17"|  
|任何其他字符|任意其他非转义字符被解释为自定义格式说明符。<br /><br /> 有关更多信息，请参见[其他字符](#Other)。|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` \-\> "14:32:17"|  
  
<a name="dSpecifier"></a>   
## “d”自定义格式说明符  
 “d”自定义格式说明符输出 <xref:System.TimeSpan.Days%2A?displayProperty=fullName> 属性的值，该值表示时间间隔中的整天数。  它会输出 <xref:System.TimeSpan> 值中的整天数，即使该值的位数大于一。  如果 <xref:System.TimeSpan.Days%2A?displayProperty=fullName> 属性的值为零，则此说明符输出“0”。  
  
 如果单独使用“d”自定义格式说明符，请指定“%d”，以确保它不被错误解释为标准格式字符串。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#3)]
 [!code-vb[Conceptual.TimeSpan.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#3)]  
  
 下面的示例阐释“d”自定义格式说明符的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#4)]
 [!code-vb[Conceptual.TimeSpan.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#4)]  
  
 [返回表首](#table)  
  
<a name="ddSpecifier"></a>   
## “dd”\-“dddddddd”自定义格式说明符  
 “dd”、“ddd”、“dddd”、“ddddd”、“dddddd”、“ddddddd”和“dddddddd”自定义格式说明符输出 <xref:System.TimeSpan.Days%2A?displayProperty=fullName> 属性的值，该值表示时间间隔中的整天数。  
  
 输出字符串包含一个由格式说明符中的“d”字符数指定的最小位数的数字，可以根据需要用前导零填充此数字。  如果天数中的位数超过格式说明符中的“d”字符的数目，则在结果字符串中输出整天数。  
  
 下面的示例使用这些格式说明符显示两个 <xref:System.TimeSpan> 值的字符串表示形式。  第一个时间间隔的天部分的值为零；第二个时间间隔的天部分的值为 365。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#5)]
 [!code-vb[Conceptual.TimeSpan.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#5)]  
  
 [返回表首](#table)  
  
<a name="hSpecifier"></a>   
## “h”自定义格式说明符  
 “h”自定义格式说明符输出 <xref:System.TimeSpan.Hours%2A?displayProperty=fullName> 属性的值，该值表示时间间隔中的未计入天部分中的整小时数。  如果 <xref:System.TimeSpan.Hours%2A?displayProperty=fullName> 属性的值为 0 到 9，则此说明符返回一位数的字符串值；如果 <xref:System.TimeSpan.Hours%2A?displayProperty=fullName> 属性的值为 10 到 23，则此说明符返回两位数的字符串值。  
  
 如果单独使用“h”自定义格式说明符，请指定“%h”，以确保它不被错误解释为标准格式字符串。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
 [!code-vb[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]  
  
 通常，在分析操作中，只包含一个数字的输入字符串被解释为天数。  可以改用“%h”自定义格式说明符以将数值字符串解释为小时数。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#8)]
 [!code-vb[Conceptual.TimeSpan.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#8)]  
  
 下面的示例阐释“h”自定义格式说明符的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#7)]
 [!code-vb[Conceptual.TimeSpan.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#7)]  
  
 [返回表首](#table)  
  
<a name="hhSpecifier"></a>   
## “hh”自定义格式说明符  
 “hh”自定义格式说明符输出 <xref:System.TimeSpan.Hours%2A?displayProperty=fullName> 属性的值，该值表示时间间隔中的未计入天部分中的整小时数。  对于从 0 到 9 的值，输出字符串包含一个前导零。  
  
 通常，在分析操作中，只包含一个数字的输入字符串被解释为天数。  可以改用“hh”自定义格式说明符以将数值字符串解释为小时数。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#9)]
 [!code-vb[Conceptual.TimeSpan.Custom#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#9)]  
  
 下面的示例阐释“hh”自定义格式说明符的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#10)]
 [!code-vb[Conceptual.TimeSpan.Custom#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#10)]  
  
 [返回表首](#table)  
  
<a name="mSpecifier"></a>   
## “m”自定义格式说明符  
 “m”自定义格式说明符输出 <xref:System.TimeSpan.Minutes%2A?displayProperty=fullName> 属性的值，该值表示时间间隔中的未计入天部分中的整分钟数。  如果 <xref:System.TimeSpan.Minutes%2A?displayProperty=fullName> 属性的值为 0 到 9，则此说明符返回一位数的字符串值；如果 <xref:System.TimeSpan.Minutes%2A?displayProperty=fullName> 属性的值的为 10 到 59，则此说明符返回两位数的字符串值。  
  
 如果单独使用“m”自定义格式说明符，请指定“%m”，以确保它不被错误解释为标准格式字符串。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
 [!code-vb[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]  
  
 通常，在分析操作中，只包含一个数字的输入字符串被解释为天数。  可以改用“%m”自定义格式说明符以将数值字符串解释为分钟数。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#11)]
 [!code-vb[Conceptual.TimeSpan.Custom#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#11)]  
  
 下面的示例阐释“m”自定义格式说明符的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#12)]
 [!code-vb[Conceptual.TimeSpan.Custom#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#12)]  
  
 [返回表首](#table)  
  
<a name="mmSpecifier"></a>   
## “mm”自定义格式说明符  
 “mm”自定义格式说明符输出 <xref:System.TimeSpan.Minutes%2A?displayProperty=fullName> 属性的值，该值表示时间间隔中的未计入小时或天部分中的整分钟数。  对于从 0 到 9 的值，输出字符串包含一个前导零。  
  
 通常，在分析操作中，只包含一个数字的输入字符串被解释为天数。  可以改用“mm”自定义格式说明符以将数值字符串解释为分钟数。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#13)]
 [!code-vb[Conceptual.TimeSpan.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#13)]  
  
 下面的示例阐释“mm”自定义格式说明符的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#14)]
 [!code-vb[Conceptual.TimeSpan.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#14)]  
  
 [返回表首](#table)  
  
<a name="sSpecifier"></a>   
## “s”自定义格式说明符  
 “s”自定义格式说明符输出 <xref:System.TimeSpan.Seconds%2A?displayProperty=fullName> 属性的值，该值表示时间间隔中的未计入小时、天或分钟部分的整秒数。  如果 <xref:System.TimeSpan.Seconds%2A?displayProperty=fullName> 属性的值为 0 到 9，则此字符串返回一位数的字符串值；如果 <xref:System.TimeSpan.Seconds%2A?displayProperty=fullName> 属性的值为 10 到 59，则此字符串返回两位数的字符串值。  
  
 如果单独使用“s”自定义格式说明符，请指定“%s”，以确保它不被错误解释为标准格式字符串。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#15)]
 [!code-vb[Conceptual.TimeSpan.Custom#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#15)]  
  
 通常，在分析操作中，只包含一个数字的输入字符串被解释为天数。  可以改用“%s”自定义格式说明符以将数值字符串解释为秒数。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#17)]
 [!code-vb[Conceptual.TimeSpan.Custom#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#17)]  
  
 下面的示例阐释“s”自定义格式说明符的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#16)]
 [!code-vb[Conceptual.TimeSpan.Custom#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#16)]  
  
 [返回表首](#table)  
  
<a name="ssSpecifier"></a>   
## “ss”自定义格式说明符  
 “ss”自定义格式说明符输出 <xref:System.TimeSpan.Seconds%2A?displayProperty=fullName> 属性的值，该值表示时间间隔中的未计入小时、天或分钟部分的整秒数。  对于从 0 到 9 的值，输出字符串包含一个前导零。  
  
 通常，在分析操作中，只包含一个数字的输入字符串被解释为天数。  可以改用“ss”自定义格式说明符以将数值字符串解释为秒数。  下面的示例进行了这方面的演示。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#18)]
 [!code-vb[Conceptual.TimeSpan.Custom#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#18)]  
  
 下面的示例阐释“ss”自定义格式说明符的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#19)]
 [!code-vb[Conceptual.TimeSpan.Custom#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#19)]  
  
 [返回表首](#table)  
  
<a name="fSpecifier"></a>   
## “f”自定义格式说明符  
 “f”自定义格式说明符输出时间间隔中的十分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，输入字符串必须只包含一个小数位。  
  
 如果单独使用“f”自定义格式说明符，请指定“%f”，以确保它不被错误解释为标准格式字符串。  
  
 下面的示例使用“f”自定义格式说明符显示 <xref:System.TimeSpan> 值中的十分之几秒。“f”首先只会用作格式说明符，然后再与自定义格式字符串中的“s”说明符一起使用。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [返回表首](#table)  
  
<a name="ffSpecifier"></a>   
## “ff”自定义格式说明符  
 “ff”自定义格式说明符输出时间间隔中的百分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，输入字符串必须只包含两个小数位。  
  
 下面的示例使用“ff”自定义格式说明符显示 <xref:System.TimeSpan> 值中的百分之几秒。“ff”首先只会用作格式说明符，然后再与自定义格式字符串中的“s”说明符一起使用。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [返回表首](#table)  
  
<a name="f3Specifier"></a>   
## “fff”自定义格式说明符  
 “fff”自定义格式说明符（带有三个“f”字符）输出时间间隔中的毫秒。  在格式设置操作中，任何其余的小数位将被截断。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，输入字符串必须只包含三个小数位。  
  
 下面的示例使用“fff”自定义格式说明符显示 <xref:System.TimeSpan> 值中的毫秒。“fff”首先只会用作格式说明符，然后再与自定义格式字符串中的“s”说明符一起使用。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [返回表首](#table)  
  
<a name="f4Specifier"></a>   
## “ffff”自定义格式说明符  
 “ffff”自定义格式说明符（带有四个“f”字符）输出时间间隔中的万分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，输入字符串必须只包含四个小数位。  
  
 下面的示例使用“ffff”自定义格式说明符显示 <xref:System.TimeSpan> 值中的万分之几秒。“ffff”首先只会用作格式说明符，然后再与自定义格式字符串中的“s”说明符一起使用。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [返回表首](#table)  
  
<a name="f5Specifier"></a>   
## “fffff”自定义格式说明符  
 “fffff”自定义格式说明符（带有五个“f”字符）输出时间间隔中的十万分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，输入字符串必须只包含五个小数位。  
  
 下面的示例使用“fffff”自定义格式说明符显示 <xref:System.TimeSpan> 值中的十万分之几秒。“fffff”首先只会用作格式说明符，然后再与自定义格式字符串中的“s”说明符一起使用。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [返回表首](#table)  
  
<a name="f6Specifier"></a>   
## “ffffff”自定义格式说明符  
 “ffffff”自定义格式说明符（带有六个“f”字符）输出时间间隔中的百万分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，输入字符串必须只包含六个小数位。  
  
 下面的示例使用“ffffff”自定义格式说明符显示 <xref:System.TimeSpan> 值中的百万分之几秒。  它首先只会用作格式说明符，然后再与自定义格式字符串中的“s”说明符一起使用。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [返回表首](#table)  
  
<a name="f7Specifier"></a>   
## “fffffff”自定义格式说明符  
 “fffffff”自定义格式说明符（带有七个“f”字符）输出时间间隔中的千万分之几秒（或小数嘀嗒数）。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，输入字符串必须只包含七个小数位。  
  
 下面的示例使用“fffffff”自定义格式说明符显示 <xref:System.TimeSpan> 值中的小数嘀嗒数。  它首先只会用作格式说明符，然后再与自定义格式字符串中的“s”说明符一起使用。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [返回表首](#table)  
  
<a name="F_Specifier"></a>   
## “F”自定义格式说明符  
 “F”自定义格式说明符输出时间间隔中的十分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  如果时间间隔的十分之几秒的值为零，则它不会包含在结果字符串中。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，可以选择显示十分之几秒数。  
  
 如果单独使用“F”自定义格式说明符，请指定“%F”，以确保它不被错误解释为标准格式字符串。  
  
 下面的示例使用“F”自定义格式说明符显示 <xref:System.TimeSpan> 值中的十分之几秒。  此外，该示例还在分析操作中使用此自定义格式说明符。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#21)]
 [!code-vb[Conceptual.TimeSpan.Custom#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#21)]  
  
 [返回表首](#table)  
  
<a name="FF_Specifier"></a>   
## “FF”自定义格式说明符  
 “FF”自定义格式说明符输出时间间隔中的百分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  如果小数部分有任何尾随零，则它们不会包含在结果字符串中。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，可以选择显示十分之几秒数和百分之几秒数。  
  
 下面的示例使用“FF”自定义格式说明符显示 <xref:System.TimeSpan> 值中的百分之几秒。  此外，该示例还在分析操作中使用此自定义格式说明符。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#22)]
 [!code-vb[Conceptual.TimeSpan.Custom#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#22)]  
  
 [返回表首](#table)  
  
<a name="F3_Specifier"></a>   
## “FFF”自定义格式说明符  
 “FFF”自定义格式说明符（带有三个“F”字符）输出时间间隔中的毫秒。  在格式设置操作中，任何其余的小数位将被截断。  如果小数部分有任何尾随零，则它们不会包含在结果字符串中。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，可以选择显示十分之几秒数、百分之几秒数和千分之几秒数。  
  
 下面的示例使用“FFF”自定义格式说明符显示 <xref:System.TimeSpan> 值中的千分之几秒。  此外，该示例还在分析操作中使用此自定义格式说明符。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#23)]
 [!code-vb[Conceptual.TimeSpan.Custom#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#23)]  
  
 [返回表首](#table)  
  
<a name="F4_Specifier"></a>   
## “FFFF”自定义格式说明符  
 “FFFF”自定义格式说明符（带有四个“F”字符）输出时间间隔中的万分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  如果小数部分有任何尾随零，则它们不会包含在结果字符串中。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，可以选择显示十分之几秒数、百分之几秒数、千分之几秒数和万分之几秒数。  
  
 下面的示例使用“FFFF”自定义格式说明符显示 <xref:System.TimeSpan> 值中的万分之几秒。  此外，该示例还在分析操作中使用“FFFF”自定义格式说明符。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#24](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#24)]
 [!code-vb[Conceptual.TimeSpan.Custom#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#24)]  
  
 [返回表首](#table)  
  
<a name="F5_Specifier"></a>   
## “FFFFF”自定义格式说明符  
 “FFFFF”自定义格式说明符（带有五个“F”字符）输出时间间隔中的十万分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  如果小数部分有任何尾随零，则它们不会包含在结果字符串中。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，可以选择显示十分之几秒数、百分之几秒数、千分之几秒数、万分之几秒数和十万分之几秒数。  
  
 下面的示例使用“FFFFF”自定义格式说明符显示 <xref:System.TimeSpan> 值中的十万分之几秒。  此外，该示例还在分析操作中使用“FFFFF”自定义格式说明符。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#25](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#25)]
 [!code-vb[Conceptual.TimeSpan.Custom#25](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#25)]  
  
 [返回表首](#table)  
  
<a name="F6_Specifier"></a>   
## “FFFFFF”自定义格式说明符  
 “FFFFFF”自定义格式说明符（带有六个“F”字符）输出时间间隔中的百万分之几秒。  在格式设置操作中，任何其余的小数位将被截断。  如果小数部分有任何尾随零，则它们不会包含在结果字符串中。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，可以选择显示十分之几秒数、百分之几秒数、千分之几秒数、万分之几秒数、十万分之几秒数和百万分之几秒数。  
  
 下面的示例使用“FFFFFF”自定义格式说明符显示 <xref:System.TimeSpan> 值中的百万分之几秒。  此外，该示例还在分析操作中使用此自定义格式说明符。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#26](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#26)]
 [!code-vb[Conceptual.TimeSpan.Custom#26](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#26)]  
  
 [返回表首](#table)  
  
<a name="F7_Specifier"></a>   
## “FFFFFFF”自定义格式说明符  
 “FFFFFFF”自定义格式说明符（带有七个“F”字符）输出时间间隔中的千万分之几秒（或小数嘀嗒数）。  如果小数部分有任何尾随零，则它们不会包含在结果字符串中。  在调用 <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> 或 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> 方法的分析操作中，可以选择在输入字符串中存在七个小数位。  
  
 下面的示例使用“FFFFFFF”自定义格式说明符显示 <xref:System.TimeSpan> 值中秒的小数部分。  此外，该示例还在分析操作中使用此自定义格式说明符。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#27](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#27)]
 [!code-vb[Conceptual.TimeSpan.Custom#27](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#27)]  
  
 [返回表首](#table)  
  
<a name="Other"></a>   
## 其他字符  
 格式字符串中的任何其他非转义字符（包括空白字符）都被解释为自定义格式说明符。  大多数情况下，存在任何其他非转义字符都会导致引发 <xref:System.FormatException>。  
  
 可以通过两种方式将文本字符包含在格式字符串中：  
  
-   用单引号将文本字符引起来（文本字符串分隔符）。  
  
-   在文本字符前面放置一个反斜杠（“\\”），它被解释为转义符。  这意味着，在 C\# 中，格式字符串必须是用 @ 引起的，或文本字符的前面必须有额外的反斜杠。  
  
     在某些情况下，在格式字符串中可能需要使用条件逻辑包括一个转义的文本。  下面的示例使用条件逻辑包括负时间间隔中的符号。  
  
     [!code-csharp[Conceptual.TimeSpan.Custom#29](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/negativevalues1.cs#29)]
     [!code-vb[Conceptual.TimeSpan.Custom#29](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/negativevalues1.vb#29)]  
  
 .NET Framework 没有为时间间隔中的分隔符定义语法。  这意味着，在格式字符串中，必须将天和小时之间的分隔符、小时和分钟之间的分隔符、分钟和秒之间的分隔符以及秒和秒的小数部分之间的分隔符全都视为字符文本。  
  
 下面的示例同时使用转义字符和单引号来定义输出字符串中包含单词“分钟”的自定义格式字符串。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#28](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/literal1.cs#28)]
 [!code-vb[Conceptual.TimeSpan.Custom#28](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/literal1.vb#28)]  
  
 [返回表首](#table)  
  
## 请参阅  
 [格式化类型](../../../docs/standard/base-types/formatting-types.md)   
 [标准 TimeSpan 格式字符串](../../../docs/standard/base-types/standard-timespan-format-strings.md)