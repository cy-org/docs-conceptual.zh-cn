---
title: "正则表达式中的限定符 | Microsoft Docs"
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
  - "正则表达式，限定符"
  - "元字符，限定符"
  - "最少的匹配限定符"
  - "正则表达式中的限定符"
  - ".NET Framework 正则表达式，限定符"
  - "限定符"
  - "惰性限定符"
ms.assetid: 36b81212-6511-49ed-a8f1-ff080415312f
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# 正则表达式中的限定符
限定符指定在输入中必须存在字符、组或字符类的多少个实例才能找到匹配项。下表列出了 .NET Framework 支持的限定符。  
  
|贪婪的限定符|惰性限定符|说明|  
|------------|-----------|--------|  
|`*`|`*?`|匹配零次或多次。|  
|`+`|`+?`|匹配一次或多次。|  
|`?`|`??`|匹配零次或一次。|  
|`{` *n* `}`|`{` *n* `}?`|准确分配*n*次|  
|`{` *n* `,}`|`{` *n* `,}?`|至少匹配 *n*次。|  
|`{` *n* `,` *m* `}`|`{` *n* `,` *m* `}?`|从 *n* 与 *m* 次。|  
  
 数量 `n` 和 `m` 是整数常数。  通常，限定符是贪婪的；它们使正则表达式引擎将尽可能多地匹配特定模式的匹配项。  在 `?` 字符后追加限定符使其成为惰性的；它使正则表达式引擎可以尽可能少的匹配匹配项。  有关贪婪限定符与惰性限定符之间差别的完整描述，请参见本主题后面部分的[贪婪限定符与惰性限定符](#Greedy)一节。  
  
> [!IMPORTANT]
>  作为输入字符串中字符数量的幂函数，嵌套限定符（例如，如正则表达式模式 `(a*)*` 的操作）可以增加正则表达式引擎必须执行的比较的数量。  关于此行为和其解决方法的更多信息，请参见 [回溯](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)。  
  
## 正则表达式限定符  
 下面几节列出了 .NET Framework 正则表达式支持的限定符。  
  
> [!NOTE]
>  如果在正则表达式模式中遇到 \*、\+、？、{ 和 } 字符，将正则表达式引擎将它们解释为限定符或限定符构造的一部分，除非它们包括在[字符类](../../../docs/standard/base-types/character-classes-in-regular-expressions.md)中。  若要将其解释为字符类之外的文本字符，必须将它们通过在前面加一个反斜杠进行转义。  例如，正则表达式模式中的字符串 `\*` 被解释为原义星号（“\*”）字符。  
  
### 匹配零次或多次：\*  
 `*` 限定符匹配前面的元素零次或多次。  它等效于 `{0,}` 限定符。  `*` 是贪婪限定符，对应的惰性限定符是 `*?`。  
  
 下面的示例演示了此正则表达式。  在输入字符串内的 9 个数字中，有 5 个与模式匹配，有 4 个（`95`、`929`、`9129` 和 `9919`）不匹配。  
  
 [!code-csharp[RegularExpressions.Quantifiers#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#1)]
 [!code-vb[RegularExpressions.Quantifiers#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#1)]  
  
 正则表达式模式的定义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`91*`|匹配后跟零或多个“1”字符的“9”。|  
|`9*`|匹配零个或多个“9”字符。|  
|`\b`|在单词边界处结束。|  
  
### 匹配一次或多次：\+  
 `+` 限定符匹配前面的元素一次或多次。  它等效于 `{1,}`。  `+` 是贪婪限定符，对应的惰性限定符是 `+?`。  
  
 例如，正则表达式 `\ban+\w*?\b` 尝试匹配以字母 `a` 开头且后跟字母 `n` 的一个或多个实例的完整单词。  下面的示例演示了此正则表达式。  该正则表达式匹配单词 `an`、`annual`、`announcement` 和 `antique`，但不匹配 `autumn` 和 `all`。  
  
 [!code-csharp[RegularExpressions.Quantifiers#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#2)]
 [!code-vb[RegularExpressions.Quantifiers#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#2)]  
  
 正则表达式模式的定义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`an+`|匹配后跟一个或多个“n”字符的“a” 。|  
|`\w*?`|匹配上字字符零次或多次，但次数尽可能少。|  
|`\b`|在单词边界处结束。|  
  
### 匹配零次或一次：?  
 `?` 限定符匹配前面的元素零次或一次。  它等效于 `{0,1}`。  `?` 是贪婪限定符，对应的惰性限定符是 `??`。  
  
 例如，正则表达式 `\ban?\b` 尝试匹配以字母 `a` 开头且后跟字母 `n` 的零个或一个实例的完整单词。  换言之，它尝试匹配单词 `a` 和 `an`。  下面的示例演示了此正则表达式。  
  
 [!code-csharp[RegularExpressions.Quantifiers#3](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#3)]
 [!code-vb[RegularExpressions.Quantifiers#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#3)]  
  
 正则表达式模式的定义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`an?`|匹配后跟零或一个“n”字符的“a” 。|  
|`\b`|在单词边界处结束。|  
  
### 精确匹配 n 次：{n}  
 `{`*n*`}`限定符准确匹配前面的元素*n* 次，其中 *n* 是任何整数。  `{`*n*`}`是贪婪限定符，对应的惰性限定符是`{`*n*`}?`。  
  
 例如，正则表达式 `\b\d+\,\d{3}\b` 尝试匹配如下字符串：先是一个字边界，然后是一个或多个十进制数字，后面再跟 3 个十进制数字，最后又是一个字边界。  下面的示例演示了此正则表达式。  
  
 [!code-csharp[RegularExpressions.Quantifiers#4](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#4)]
 [!code-vb[RegularExpressions.Quantifiers#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#4)]  
  
 正则表达式模式的定义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`\d+`|匹配一个或多个十进制数字。|  
|`\,`|匹配逗号字符。|  
|`\d{3}`|匹配三个十进制数字。|  
|`\b`|在单词边界处结束。|  
  
### 至少匹配 n 次：{n,}  
 The `{`*n*`,}`限定符匹配前面的元素至少*n* 次，其中*n* 是任何整数。  `{`*n*`,}`是贪婪限定符，对应的惰性限定符是`{`*n*`}?`。  
  
 例如，正则表达式 `\b\d{2,}\b\D+` 尝试匹配如下字符串：先是一个字边界，然后是至少 2 个数字，然后再跟一个字边界和一个非数字字符。  下面的示例演示了此正则表达式。  该正则表达式不能匹配短语 `"7 days"`，原因是该短语只包含一个十进制数字；但该表达式可成功匹配短语 `"10 weeks and 300 years"`。  
  
 [!code-csharp[RegularExpressions.Quantifiers#5](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#5)]
 [!code-vb[RegularExpressions.Quantifiers#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#5)]  
  
 正则表达式模式的定义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`\d{2,}`|匹配至少量个十进制数字。|  
|`\b`|与字边界匹配。|  
|`\D+`|匹配至少一个非十进制数字。|  
  
### 匹配 n 到 m 次：{n，m}  
 `{` *n* `,` *m* `}`限定符匹配前面的元素至少  *n*次，但不超过*m*次，其中*n*和*m* 为整数。  `{`*n*`,`*m*`}`是贪婪限定符，对应的惰性限定符是`{`*n*`,`*m*`}?`。  
  
 在下面的示例中，正则表达式 `(00\s){2,4}` 尝试匹配两个相连的零和一个紧随的空格，且匹配 2 到 4 个实例。  注意输入字符串的最后包含此模式 5 次，而不是最大的 4 次。  但是，仅此子字符串的开头（一直到空格和第五对 0）与该正则表达式模式匹配。  
  
 [!code-csharp[RegularExpressions.Quantifiers#6](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#6)]
 [!code-vb[RegularExpressions.Quantifiers#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#6)]  
  
### 匹配零次或多次（惰性匹配）：\*?  
 `*?` 限定符可以匹配前导元素一次或多次，但次数尽可能少。  它是与贪婪限定符 `*` 对应的惰性部分。  
  
 在下面的示例中，正则表达式 `\b\w*?oo\w*?\b` 与包含字符串 `oo` 的所有词匹配。  
  
 [!code-csharp[RegularExpressions.Quantifiers#7](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#7)]
 [!code-vb[RegularExpressions.Quantifiers#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#7)]  
  
 正则表达式模式的定义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`\w*?`|匹配零个或多个字字符，但字符尽可能少。|  
|`oo`|匹配字符串“oo”。|  
|`\w*?`|匹配零个或多个字字符，但字符尽可能少。|  
|`\b`|在单词边界处结束。|  
  
### 匹配一次或多次（惰性匹配）：\+?  
 `+?` 限定符可以匹配前导元素一次或多次，但次数尽可能少。  它是与贪婪限定符 `+` 对应的惰性部分。  
  
 例如，正则表达式 `\b\w+?\b` 匹配由字边界分隔的一个或多个字符。  下面的示例演示了此正则表达式。  
  
 [!code-csharp[RegularExpressions.Quantifiers#8](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#8)]
 [!code-vb[RegularExpressions.Quantifiers#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#8)]  
  
### 匹配零次或一次（惰性匹配）：??  
 `??` 限定符可以匹配前导元素零次或一次，但次数尽可能少。  它是与贪婪限定符 `?` 对应的惰性部分。  
  
 例如，正则表达式 `^\s*(System.)??Console.Write(Line)??\(??` 尝试匹配 "Console.Write" 或者 "Console.WriteLine" 字符串。  字符串还可以在“控制台”前包含“系统.”，它后面可以跟着左括号。  该字符串必须位于一行的开头，不过它的前面可以有空白。  下面的示例演示了此正则表达式。  
  
 [!code-csharp[RegularExpressions.Quantifiers#9](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#9)]
 [!code-vb[RegularExpressions.Quantifiers#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#9)]  
  
 正则表达式模式的定义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`^`|匹配输入字符串的开始部分。|  
|`\s*`|匹配零个或多个空白字符。|  
|`(System.)??`|匹配字符串“System.”的零个或一个匹配项。|  
|`Console.Write`|匹配字符串"Console.Write"。|  
|`(Line)??`|匹配字符串"Line"零次或一次。|  
|`\(??`|匹配左括号的零个或一个匹配项。|  
  
### 精确匹配 n 次（惰性匹配）：{n}?  
 `{`*n*`}?`限定符准确匹配前面的元素`n` 次，其中 *n* 是任何整数。  它是与贪婪限定符`{`*n*`}+`对应的惰性部分。  
  
 在下面的示例中，使用正则表达式 `\b(\w{3,}?\.){2}?\w{3,}?\b` 标识网站地址。  请注意它与“www.microsoft.com”和“msdn.microsoft.com”相匹配，但与“mywebsite”或“mycompany.com”不匹配。  
  
 [!code-csharp[RegularExpressions.Quantifiers#10](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#10)]
 [!code-vb[RegularExpressions.Quantifiers#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#10)]  
  
 正则表达式模式的定义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`(\w{3,}?\.)`|至少匹配 3 个字字符，但字符尽可能少，后跟圆点或句点字符。  这是第一个捕获组。|  
|`(\w{3,}?\.){2}?`|与第一个组中的模式匹配两次，但次数尽可能少。|  
|`\b`|在单词边界处结束匹配。|  
  
### 至少匹配 n 次（惰性匹配）：n,}?  
 `{` *n* `,}?`限定符匹配前面的元素至少 `n`次，其中*n* 是任何整数，但是次数尽可能少。  它是与贪婪限定符`{`*n*`,}`对应的惰性部分。  
  
 要查看实例，请参阅上一节中`{`*n*`}?` 限定符的示例。  该例中的正则表达式使用`{`*n*`,}`限定符来匹配含有至少 3 个字符且这些字符后面跟有句点的字符串。  
  
### 匹配 n 到 m 次（惰性匹配）：{n，m} ?  
 `{` *n* `,` *m* `}?`限定符匹配前面的元素  `n`和`m` 次，其中*n*和*m*为整数，但是次数尽可能少。  它是与贪婪限定符 `{`*n*`,`*m*`}`对应的惰性部分。  
  
 在下面的示例中，正则表达式 `\b[A-Z](../../../amples/snippets/visualbasic/VS_Snippets_Remoting/SoapAttributes1/VB/s.vb){1,10}?[.!?]` 匹配包含一到十个词的句子。  该示例匹配输入字符串中除了包含 18 个单词的那个句子之外的所有句子。  
  
 [!code-csharp[RegularExpressions.Quantifiers#12](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#12)]
 [!code-vb[RegularExpressions.Quantifiers#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#12)]  
  
 正则表达式模式的定义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`[A-Z]`|匹配从 A 到 Z 的大写字符。|  
|`(\w*\s+)`|匹配零个或多个字字符，后跟一个或多个空白字符。  这是第一个捕获组。|  
|`{1,10}?`|匹配上一个模式的次数介于 1 和 10 之间，但次数尽可能少。|  
|`[.!?]`|匹配标点字符“.”、“\!”或“?”中的任何一个。|  
  
<a name="Greedy"></a>   
## 贪婪限定符与惰性限定符  
 一些限定符有两种版本：  
  
-   贪婪版本。  
  
     贪婪限定符尝试尽可能多地匹配元素。  
  
-   非贪婪（惰性）版本。  
  
     非贪婪限定符尝试尽可能少地匹配元素。  只需添加 `?`，便可以将贪婪限定符转换为惰性限定符。  
  
 考虑一个简单的正则表达式，旨在从信用卡号之类的数字串中提取最后四位数。  使用 `*` 贪婪限定符的正则表达式版本为 `\b.*([0-9]{4})\b`。  但是，如果一个字符串包含两组数字，则此正则表达式只与第二组数字的最后四位数匹配，如下面的示例所示。  
  
 [!code-csharp[RegularExpressions.Quantifiers.Greedy#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/cs/Greedy.cs#1)]
 [!code-vb[RegularExpressions.Quantifiers.Greedy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/vb/Greedy.vb#1)]  
  
 该正则表达式未能匹配第一个卡号，因为 `*` 限定符尝试在整个字符串中尽可能多地匹配前面的元素，因此它在字符串的末尾找到了匹配项。  
  
 这不是所需要的行为。  相反，您可以使用 `*?` ``  惰性限定符从两个号码提取数字，如下面的示例所示的数字。  
  
 [!code-csharp[RegularExpressions.Quantifiers.Greedy#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/cs/Greedy.cs#2)]
 [!code-vb[RegularExpressions.Quantifiers.Greedy#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/vb/Greedy.vb#2)]  
  
 在大多数情况下，带有贪婪限定符和惰性限定符的正则表达式将返回相同的匹配项。  在与通配符 \(`.`\) 元字符（该元字符匹配任何字符）一起使用时，它们多数情况下会返回不同的结果。  
  
## 限定符和空匹配  
 限定符`*`, `+`,和 `{`*n*`,`*m*`}` 以及他们的贪婪限定符在找到最小捕获数后为空匹配后不再重复。  此规则会阻止限定符在可能的群组捕获的最大数目为无限大或接近无限大时进入空子表达式匹配的无限循环。  
  
 例如，下面的代码显示调用正则表达式模式 `(a?)*` 的 <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=fullName> 方法的结果，将匹配零个或一个 "a" 字符零次或多次。  请注意，单个捕获组捕获每个“a”以及 <xref:System.String.Empty?displayProperty=fullName>，但没有第二个空匹配，因为第一个空匹配导致数量值停止重复。  
  
 [!code-csharp[RegularExpressions.Quantifiers.EmptyMatch#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/cs/emptymatch1.cs#1)]
 [!code-vb[RegularExpressions.Quantifiers.EmptyMatch#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/vb/emptymatch1.vb#1)]  
  
 要查看定义最小和最大捕获数与定义固定捕获数的捕获组之间的实际差异，请考虑正则表达式模式 `(a\1|(?(1)\1)){0,2}` 和 `(a\1|(?(1)\1)){2}`。  这两个正则表达式都包含一个捕获组，如下表中所定义。  
  
|模式|说明|  
|--------|--------|  
|`(a\1`|随着第一次捕获组的值匹配 "a"……|  
|`&#124;(?(1)`|… 或测试是否已定义第一个捕获组。（请注意，`(?(1)` 构造不定义捕获组。）|  
|`\1))`|如果第一个捕获分组存在，则与其值相匹配。  如果分组不存在，则分组将与 <xref:System.String.Empty?displayProperty=fullName> 相匹配。|  
  
 第一个正则表达式试图在零至两倍之间匹配此模式；第二个则完全是两倍。  由于第一个模式在第一次捕获 <xref:System.String.Empty?displayProperty=fullName> 时达到其最小捕获量，因此它绝不会重复尝试匹配 `a\1`；`{0,2}` 限定符只允许在最后的迭代中存在空匹配。  与之相反，第二个常规表达式与“a”匹配，因为它会再一次计算 `a\1`；最小迭代次数为 2，可强制引擎在空匹配后重复。  
  
 [!code-csharp[RegularExpressions.Quantifiers.EmptyMatch#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/cs/emptymatch4.cs#2)]
 [!code-vb[RegularExpressions.Quantifiers.EmptyMatch#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/vb/emptymatch4.vb#2)]  
  
## 请参阅  
 [正则表达式语言 \- 快速参考](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)   
 [回溯](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)