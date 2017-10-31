---
title: "正则表达式语言 - 快速参考 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "VS.RegularExpressionBuilder"
helpviewer_keywords: 
  - ".NET Framework 正则表达式, 语言元素"
  - "速查表"
  - "分析带有正则表达式的文本, 语言元素"
  - "正则表达式的模式匹配, 语言元素"
  - "正则表达式速查表"
  - "正则表达式 [.NET Framework]"
  - "正则表达式, 语言元素"
  - "用正则表达式搜索, 语言元素"
ms.assetid: 930653a6-95d2-4697-9d5a-52d11bb6fd4c
caps.latest.revision: 56
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 56
---
# 正则表达式语言 - 快速参考
<a name="top"></a> 正则表达式是正则表达式引擎尝试匹配输入文本的一种模式。 模式由一个或多个字符文本、运算符或构造组成。  有关简单介绍，请参阅 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)。  
  
 此快速参考中的每一节都列出了可用于定义正则表达式的字符、运算符和构造的一种特定类别：  
  
 [字符转义](#character_escapes)  
 [字符类](#character_classes)  
 [定位点](#atomic_zerowidth_assertions)  
 [分组构造](#grouping_constructs)  
 [数量词](#quantifiers)  
 [反向引用构造](#backreference_constructs)  
 [替换构造](#alternation_constructs)  
 [替代](#substitutions)  
 [正则表达式选项](#options)  
 [其他构造](#miscellaneous_constructs)  
  
 我们还提供此信息的两种格式，你可以下载和打印，以便参考：  
  
 [以 Word \(.docx\) 格式下载](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)  
[以 PDF \(.pdf\) 格式下载](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)  
  
<a name="character_escapes"></a>   
## 字符转义  
 正则表达式中的反斜杠字符 \(\\\) 指示其后跟的字符是特殊字符（如下表所示），或应按原义解释该字符。 有关详细信息，请参阅[字符转义](../../../docs/standard/base-types/character-escapes-in-regular-expressions.md)。  
  
|转义字符|描述|模式|匹配|  
|----------|--------|--------|--------|  
|`\a`|与报警 \(bell\) 符 \\u0007 匹配。|`\a`|“Error\!”\+“\\u0007”中的 “\\u0007”|  
|`\b`|在字符类中，与退格键 \\u0008 匹配。|`[\b]{3,}`|“\\b\\b\\b\\b”中的“\\b\\b\\b\\b”|  
|`\t`|与制表符 \\u0009 匹配。|`(\w+)\t`|“item1\\titem2\\t”中的“item1\\t”和“item2\\t”|  
|`\r`|与回车符 \\u000D 匹配。 （`\r` 与换行符 `\n` 不是等效的。）|`\r\n(\w+)`|“\\r\\nThese are\\ntwo lines.”中的“\\r\\nThese”|  
|`\v`|与垂直制表符 \\u000B 匹配。|`[\v]{2,}`|“\\v\\v\\v”中的“\\v\\v\\v”|  
|`\f`|与换页符 \\u000C 匹配。|`[\f]{2,}`|“\\f\\f\\f”中的“\\f\\f\\f”|  
|`\n`|与换行符 \\u000A 匹配。|`\r\n(\w+)`|“\\r\\nThese are\\ntwo lines.”中的“\\r\\nThese”|  
|`\e`|与转义符 \\u001B 匹配。|`\e`|“\\x001B”中的“\\x001B”|  
|`\` *nnn*|使用八进制表示形式指定字符（*nnn* 由二位或三位数字组成）。|`\w\040\w`|“a bc d”中的<br /><br /> “a b”和“c d”|  
|`\x` *nn*|使用十六进制表示形式指定字符（*nn* 恰好由两位数字组成）。|`\w\x20\w`|“a bc d”中的<br /><br /> “a b”和“c d”|  
|`\c` *X*<br /><br /> `\c` *x*|匹配 *X* 或 *x* 指定的 ASCII 控件字符，其中 *X* 或 *x* 是控件字符的字母。|`\cC`|“\\x0003”中的“\\x0003”\(Ctrl\-C\)|  
|`\u` *nnnn*|使用十六进制表示形式匹配 Unicode 字符（由 *nnnn* 正确表示的四位数）。|`\w\u0020\w`|“a bc d”中的<br /><br /> “a b”和“c d”|  
|`\`|在后面带有不识别为本主题的此表和其他表中的转义符的字符时，与该字符匹配。 例如，`\*` 与 `\x2A` 相同，而 `\.` 与 `\x2E` 相同。 这允许正则表达式引擎区分语言元素（如 \* 或 ?） 和字符文本（用 `\*` 或 `\?` 表示）。|`\d+[\+-x\*]\d+`|“\(2\+2\) \* 3\*9”中的“2\+2”和“3\*9”|  
  
 [返回页首](#top)  
  
<a name="character_classes"></a>   
## 字符类  
 字符类与一组字符中的任何一个字符匹配。 字符类包括下表中列出的语言元素。 有关更多信息，请参见[字符类](../../../docs/standard/base-types/character-classes-in-regular-expressions.md)。  
  
|字符类|描述|模式|匹配|  
|---------|--------|--------|--------|  
|`[` *character\_group* `]`|匹配 *character\_group* 中的任何单个字符。 默认情况下，匹配区分大小写。|`[ae]`|“gray”中的“a”<br /><br /> “lane”中的“a”和“e”|  
|`[^` *character\_group* `]`|求反：与不在 *character\_group* 中的任何单个字符匹配。 默认情况下，*character\_group* 中的字符区分大小写。|`[^aei]`|“reign”中的“r”、“g”和“n”|  
|`[` *第一个* `-` *last* `]`|字符范围：与从*第一个*到*最后一个*的范围中的任何单个字符匹配。|`[A-Z]`|“AB123”中的“A”和“B”|  
|`.`|通配符：与除 \\n 之外的任何单个字符匹配。<br /><br /> 若要匹配文本句点字符（. 或 `\u002E`），你必须在该字符前面加上转义符 \(`\.`\)。|`a.e`|“nave”中的“ave”<br /><br /> “water”中的“ate”|  
|`\p{` *name* `}`|与 *name* 指定的 Unicode 通用类别或命名块中的任何单个字符匹配。|`\p{Lu}`<br /><br /> `\p{IsCyrillic}`|“City Lights”中的“C”和“L”<br /><br /> “ДЖem”中的“Д”和“Ж”|  
|`\P{` *name* `}`|与不在 *name* 指定的 Unicode 通用类别或命名块中的任何单个字符匹配。|`\P{Lu}`<br /><br /> `\P{IsCyrillic}`|“City”中的“i”、“t”和“y”<br /><br /> “ДЖem”中的“e”和“m”|  
|`\w`|与任何单词字符匹配。|`\w`|“ID A1.3”中的“I”、“D”、“A”、“1”和“3”|  
|`\W`|与任何非单词字符匹配。|`\W`|“ID A1.3”中的“ ”、“.”|  
|`\s`|与任何空白字符匹配。|`\w\s`|“ID A1.3”中的“D”|  
|`\S`|与任何非空白字符匹配。|`\s\S`|" \_" in "int \_\_ctr"|  
|`\d`|与任何十进制数字匹配。|`\d`|“4 \= IV”中的“4”|  
|`\D`|匹配不是十进制数的任意字符。|`\D`|“4 \= IV”中的“ ”、“\=”、“ ”、“I”和“V”|  
  
 [返回页首](#top)  
  
<a name="atomic_zerowidth_assertions"></a>   
## 定位点  
 定位点或原子零宽度断言会使匹配成功或失败，具体取决于字符串中的当前位置，但它们不会使引擎在字符串中前进或使用字符。 下表中列出的元字符是定位点。 有关更多信息，请参见[定位点](../../../docs/standard/base-types/anchors-in-regular-expressions.md)。  
  
|断言|描述|模式|匹配|  
|--------|--------|--------|--------|  
|`^`|匹配必须从字符串或一行的开头开始。|`^\d{3}`|“901”<br /><br /> “901\-”|  
|`$`|匹配必须出现在字符串的末尾或出现在行或字符串末尾的 `\n` 之前。|`-\d{3}$`|“\-333”<br /><br /> “\-333”|  
|`\A`|匹配必须出现在字符串的开头。|`\A\d{3}`|“901”<br /><br /> “901\-”|  
|`\Z`|匹配必须出现在字符串的末尾或出现在字符串末尾的 `\n` 之前。|`-\d{3}\Z`|“\-333”<br /><br /> “\-333”|  
|`\z`|匹配必须出现在字符串的末尾。|`-\d{3}\z`|“\-333”<br /><br /> “\-333”|  
|`\G`|匹配必须出现在上一个匹配结束的地方。|`\G\(\d\)`|“\(1\)\(3\)\(5\)\[7\]\(9\)”中的“\(1\)”、“\(3\)”、“\(5\)”|  
|`\b`|匹配必须出现在 `\w`（字母数字）和 `\W`（非字母数字）字符之间的边界上。|`\b\w+\s\w+\b`|“them theme them them”中的“them theme”、“them them”|  
|`\B`|匹配不得出现在 `\b` 边界上。|`\Bend\w*\b`|“end sends endure lender”中的“ends”和“ender”|  
  
 [返回页首](#top)  
  
<a name="grouping_constructs"></a>   
## 分组构造  
 分组构造描述了正则表达式的子表达式，通常用于捕获输入字符串的子字符串。 分组构造包括下表中列出的语言元素。 有关详细信息，请参阅[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)。  
  
|分组构造|描述|模式|匹配|  
|----------|--------|--------|--------|  
|`(` *子表达式* `)`|捕获匹配的子表达式并将其分配到一个从 1 开始的序号中。|`(\w)\1`|“deep”中的“ee”|  
|`(?<` *名称* `>` *子表达式*`)`|将匹配的子表达式捕获到一个命名组中。|`(?<double>\w)\k<double>`|“deep”中的“ee”|  
|`(?<` *名称 1* `-` *名称 2* `>` *子表达式*`)`|定义平衡组定义。 有关详细信息，请参阅[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)中的“平衡组定义”部分。|`(((?'Open'\()[^\(\)]*)+((?'Close-Open'\))[^\(\)]*)+)*(?(Open)(?!))$`|“3\+2^\(\(1\-3\)\*\(3\-1\)\)”中的“\(\(1\-3\)\*\(3\-1\)\)”|  
|`(?:` *子表达式*`)`|定义非捕获组。|`Write(?:Line)?`|“Console.WriteLine\(\)”中的“WriteLine”<br /><br /> “Console.Write\(value\)”中的“Write”|  
|`(?imnsx-imnsx:` *子表达式*`)`|应用或禁用*子表达式*中指定的选项。 有关详细信息，请参阅[正则表达式选项](../../../docs/standard/base-types/regular-expression-options.md)。|`A\d{2}(?i:\w+)\b`|“A12xl A12XL a12xl”中的“A12xl”和“A12XL”|  
|`(?=` *子表达式*`)`|零宽度正预测先行断言。|`\w+(?=\.)`|“He is. The dog ran. The sun is out.”中的“is”、“ran”和“out”|  
|`(?!` *子表达式*`)`|零宽度负预测先行断言。|`\b(?!un)\w+\b`|“unsure sure unity used”中的“sure”和“used”|  
|`(?<=` *子表达式*`)`|零宽度正回顾后发断言。|`(?<=19)\d{2}\b`|“1851 1999 1950 1905 2003”中的“99”、“50”和“05”|  
|`(?<!` *子表达式*`)`|零宽度负回顾后发断言。|`(?<!19)\d{2}\b`|“1851 1999 1950 1905 2003”中的“51”和“03”|  
|`(?>` *子表达式*`)`|非回溯（也称为“贪婪”）子表达式。|`[13579](?>A+B+)`|“1ABB 3ABBC 5AB 5AC”中的“1ABB”、“3ABB”和“5AB”|  
  
 [返回页首](#top)  
  
<a name="quantifiers"></a>   
## 数量词  
 限定符指定在输入字符串中必须存在上一个元素（可以是字符、组或字符类）的多少个实例才能出现匹配项。 限定符包括下表中列出的语言元素。 有关更多信息，请参见[数量词](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md)。  
  
|限定符|描述|模式|匹配|  
|---------|--------|--------|--------|  
|`*`|匹配上一个元素零次或多次。|`\d*\.\d`|“.0”，“19.9”和“219.9”|  
|`+`|匹配上一个元素一次或多次。|`"be+"`|“been”中的“bee”，“bent”中的“be”|  
|`?`|匹配上一个元素零次或一次。|`"rai?n"`|“ran”和“rain”|  
|`{` *n* `}`|匹配上一个元素恰好 *n* 次。|`",\d{3}"`|“1,043.6”中的“,043”，“9,876,543,210”中的“,876”、“,543”和“,210”|  
|`{` *n* `,}`|匹配上一个元素至少 *n* 次。|`"\d{2,}"`|“166”，“29”和“1930”|  
|`{` *n* `,` *m* `}`|匹配上一个元素至少 *n* 次，但不多于 *m* 次。|`"\d{3,5}"`|“166”、“17668”<br /><br /> “193024”中的“19302”|  
|`*?`|匹配上一个元素零次或多次，但次数尽可能少。|`\d*?\.\d`|“.0”，“19.9”和“219.9”|  
|`+?`|匹配上一个元素一次或多次，但次数尽可能少。|`"be+?"`|“been”中的“be”，“bent”中的“be”|  
|`??`|匹配上一个元素零次或一次，但次数尽可能少。|`"rai??n"`|“ran”和“rain”|  
|`{` *n* `}?`|匹配前面的元素恰好 *n* 次。|`",\d{3}?"`|“1,043.6”中的“,043”，“9,876,543,210”中的“,876”、“,543”和“,210”|  
|`{` *n* `,}?`|匹配上一个元素至少 *n* 次，但次数尽可能少。|`"\d{2,}?"`|“166”，“29”和“1930”|  
|`{` *n* `,` *m* `}?`|匹配上一个元素的次数介于 *n* 和 *m* 之间，但次数尽可能少。|`"\d{3,5}?"`|“166”、“17668”<br /><br /> “193024”中的“193”、“024”|  
  
 [返回页首](#top)  
  
<a name="backreference_constructs"></a>   
## 反向引用构造  
 反向引用允许在同一正则表达式中随后标识以前匹配的子表达式。 下表列出了 .NET Framework 的正则表达式支持的反向引用构造。 有关详细信息，请参阅[反向引用构造](../../../docs/standard/base-types/backreference-constructs-in-regular-expressions.md)。  
  
|反向引用构造|描述|模式|匹配|  
|------------|--------|--------|--------|  
|`\` *数值*|后向引用。 匹配编号子表达式的值。|`(\w)\1`|“seek”中的“ee”|  
|`\k<` *name* `>`|命名后向引用。 匹配命名表达式的值。|`(?<char>\w)\k<char>`|“seek”中的“ee”|  
  
 [返回页首](#top)  
  
<a name="alternation_constructs"></a>   
## 替换构造  
 替换构造用于修改正则表达式以启用 either\/or 匹配。 这些构造包括下表中列出的语言元素。 有关详细信息，请参阅[备用构造](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md)。  
  
|替换构造|描述|模式|匹配|  
|----------|--------|--------|--------|  
|`&#124;`|匹配以竖线 \(&#124;\) 字符分隔的任何一个元素。|`th(e&#124;is&#124;at)`|“this is the day.”中的“the”和“this” "|  
|`(?(` *表达式* `)` *是* `&#124;` *no* `)`|如果正则表达式模式由 *expression* 匹配指定，则匹配 *yes*；否则，匹配可选 *no* 部分。*expression* 被解释为零宽度断言。|`(?(A)A\d{2}\b&#124;\b\d{3}\b)`|“A10 C103 910”中的“A10”和“910”|  
|`(?(` *name* `)` *是* `&#124;` *no* `)`|如果 *name*（已命名或已编号的捕获组）具有匹配，则匹配 *yes*；否则，匹配可选 *no*。|`(?<quoted>")?(?(quoted).+?"&#124;\S+\s)`|“Dogs.jpg "Yiska playing.jpg"”中的 Dogs.jpg 和 "Yiska playing.jpg"|  
  
 [返回页首](#top)  
  
<a name="substitutions"></a>   
## 替代  
 替换是替换模式中支持的正则表达式语言元素。 有关更多信息，请参见[替代](../../../docs/standard/base-types/substitutions-in-regular-expressions.md)。 下表中列出的元字符是原子零宽度断言。  
  
|字符|描述|模式|替换模式|输入字符串|结果字符串|  
|--------|--------|--------|----------|-----------|-----------|  
|`$` *数值*|替换按组 *number* 匹配的子字符串。|`\b(\w+)(\s)(\w+)\b`|`$3$2$1`|"one two"|"two one"|  
|`${` *name* `}`|替换按命名组 *name* 匹配的子字符串。|`\b(?<word1>\w+)(\s)(?<word2>\w+)\b`|`${word2} ${word1}`|"one two"|"two one"|  
|`$$`|替换字符“$”。|`\b(\d+)\s?USD`|`$$$1`|“103 USD”|“$103”|  
|`$&`|替换整个匹配项的一个副本。|`\$?\d*\.?\d+`|`**$&**`|"$1.30"|“\*\*$1.30\*\*”|  
|`$``|替换匹配前的输入字符串的所有文本。|`B+`|`$``|“AABBCC”|“AAAACC”|  
|`$'`|替换匹配后的输入字符串的所有文本。|`B+`|`$'`|“AABBCC”|“AACCCC”|  
|`$+`|替换最后捕获的组。|`B+(C+)`|`$+`|“AABBCCDD”|AACCDD|  
|`$_`|替换整个输入字符串。|`B+`|`$_`|“AABBCC”|“AAAABBCCCC”|  
  
 [返回页首](#top)  
  
<a name="options"></a>   
## 正则表达式选项  
 可以指定控制正则表达式引擎如何解释正则表达式模式的选项。 其中的许多选项可以指定为内联（在正则表达式模式中）或指定为一个或多个 <xref:System.Text.RegularExpressions.RegexOptions> 常量。 本快速参考仅列出内联选项。 有关内联和 <xref:System.Text.RegularExpressions.RegexOptions> 选项的详细信息，请参阅文章[正则表达式选项](../../../docs/standard/base-types/regular-expression-options.md)。  
  
 可通过两种方式指定内联选项：  
  
-   通过使用[杂项构造](../../../docs/standard/base-types/miscellaneous-constructs-in-regular-expressions.md)`(?imnsx-imnsx)`，可以用选项或选项组前的减号 \(\-\) 关闭这些选项。 例如，`(?i-mn)` 启用不区分大小写的匹配 \(`i`\)，关闭多行模式 \(`m`\) 并关闭未命名的组捕获 \(`n`\)。 该选项自定义选项的点开始应用于此正则表达式，且持续有效直到模式结束或者到另一构造反转此选项的点。  
  
-   通过使用[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)`(?imnsx-imnsx:`*子表达式*`)`（只定义指定组的选项）。  
  
 .NET Framework 正则表达式引擎支持以下内联选项。  
  
|选项|描述|模式|匹配|  
|--------|--------|--------|--------|  
|`i`|使用不区分大小写的匹配。|`\b(?i)a(?-i)a\w+\b`|“aardvark AAAuto aaaAuto Adam breakfast”中的“aardvark”、“aaaAuto”|  
|`m`|使用多行模式。`^` 和 `$` 匹配行的开头和结尾，但不匹配字符串的开头和结尾。|有关示例，请参阅[正则表达式选项](../../../docs/standard/base-types/regular-expression-options.md)中的“多行模式”部分。||  
|`n`|不捕获未命名的组。|有关示例，请参阅[正则表达式选项](../../../docs/standard/base-types/regular-expression-options.md)中的“仅显式捕获”部分。||  
|`s`|使用单行模式。|有关示例，请参阅[正则表达式选项](../../../docs/standard/base-types/regular-expression-options.md)中的“单行模式”部分。||  
|`x`|忽略正则表达式模式中的非转义空白。|`\b(?x) \d+ \s \w+`|“1 aardvark 2 cats IV centurions”中的“1 aardvark”、“2 cats”|  
  
 [返回页首](#top)  
  
<a name="miscellaneous_constructs"></a>   
## 其他构造  
 其他构造可修改某个正则表达式模式或提供有关该模式的信息。 下表列出了 .NET Framework 支持的其他构造。 有关详细信息，请参阅[其他构造](../../../docs/standard/base-types/miscellaneous-constructs-in-regular-expressions.md)。  
  
|构造|定义|示例|  
|--------|--------|--------|  
|`(?imnsx-imnsx)`|在模式中间对诸如不区分大小写这样的选项进行设置或禁用。 有关详细信息，请参阅[正则表达式选项](../../../docs/standard/base-types/regular-expression-options.md)。|`\bA(?i)b\w+\b` 匹配“ABA Able Act”中的“ABA”和“Able”|  
|`(?#` *注释*`)`|内联注释。 该注释在第一个右括号处终止。|`\bA(?#Matches words starting with A)\w+\b`|  
|`#` \[至行尾\]|X 模式注释。 该注释以非转义的 `#` 开头，并继续到行的结尾。|`(?x)\bA\w+\b#Matches words starting with A`|  
  
## 请参阅  
 <xref:System.Text.RegularExpressions?displayProperty=fullName>   
 <xref:System.Text.RegularExpressions.Regex>   
 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)   
 [正则表达式类](../../../docs/standard/base-types/the-regular-expression-object-model.md)   
 [正则表达式示例](../../../docs/standard/base-types/regular-expression-examples.md)   
 [正则表达式 — 快速参考（以 Word 格式下载）](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)   
 [正则表达式 — 快速参考（以 PDF 格式下载）](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)