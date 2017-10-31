---
title: "正则表达式中的其他构造 | Microsoft Docs"
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
  - ".NET Framework 正则表达式, 其他构造"
  - "构造, 杂项"
  - "正则表达式, 其他构造"
ms.assetid: 7d10d11f-680f-4721-b047-fb136316b4cd
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 正则表达式中的其他构造
.NET Framework 中的正则表达式包括三个杂项语言构造。  一个允许您在正则表达式模式中间启用或禁用特定匹配选项。  剩余的两个使您可以在正则表达式中包含注释。  
  
## 内联选项  
 可以使用此语法，为部分正则表达式设置或禁用特定模式匹配选项  
  
```  
(?imnsx-imnsx)  
```  
  
 在问号后面列出想要启用的选项，在减号后面列出想要禁用的选项。  下表对每个选项进行了描述。  有关每个选项的详细信息，请参阅[正则表达式选项](../../../docs/standard/base-types/regular-expression-options.md)。  
  
|选项|说明|  
|--------|--------|  
|`i`|不区分大小写的匹配。|  
|`m`|多行模式。|  
|`n`|仅显式捕获。（圆括号不充当捕获组\)。|  
|`s`|单行模式。|  
|`x`|忽略非转义的空白并允许 x 模式注释。|  
  
 在封闭组结束之前，`(?imnsx-imnsx)` 构造定义的正则表达式选项中的任何更改一直保持有效。  
  
> [!NOTE]
>  `(?imnsx-imnsx:` *subexpression* `)`分组构造为子表达式提供相同功能。  有关详细信息，请参阅[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)。  
  
 下面的示例使用 `i`、`n` 以及 `x` 选项启用区分大小写和显式捕获，并忽略正则表达式中间的正则表达式模式中的空白。  
  
 [!code-csharp[RegularExpressions.Language.Miscellaneous#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.miscellaneous/cs/miscellaneous1.cs#1)]
 [!code-vb[RegularExpressions.Language.Miscellaneous#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.miscellaneous/vb/miscellaneous1.vb#1)]  
  
 该示例定义两个正则表达式。  第一个 `\b(D\w+)\s(d\w+)\b`，匹配以大写的“D”和小写“d”开头的两个连续单词。  第二个的正则表达式 `\b(D\w+)(?ixn) \s (d\w+) \b`，使用内联选项来修改此模式，如下表所述。  结果的比较可以确定 `(?ixn)` 构造的效果。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`(D\w+)`|匹配后跟一个或多个字符的大写“D”。  这是第一个捕获组。|  
|`(?ixn)`|此后，进行不区分大小写的比较，仅进行显式捕获，并忽略正则表达式模式中的空白。|  
|`\s`|与空白字符匹配。|  
|`(d\w+)`|匹配后跟一个或多个字字符的大写或小写“d”。  未捕获此组，因为已启用 `n`（显式捕获）选项。|  
|`\b`|与字边界匹配。|  
  
## 内联注释  
 `(?#`  *comment* `)`构造可以在正则表达式中包括内联注释。  尽管批注包含在 <xref:System.Text.RegularExpressions.Regex.ToString%2A?displayProperty=fullName> 方法返回的字符串中，但正则表达式引擎不会使用匹配的模式中注释的任何部分。  该注释在第一个右括号处终止。  
  
 下面的示例重复来自上一节示例的第一正则表达式模式。  它将两个内嵌批注添加到正则表达式，指示比较是否区分大小写。  正则表达式模式 `\b((?# case-sensitive comparison)D\w+)\s((?#case-insensitive comparison)d\w+)\b` 按如下方式定义。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始。|  
|`(?# case-sensitive comparison)`|注释。  它不影响模式匹配行为。|  
|`(D\w+)`|匹配后跟一个或多个字符的大写“D”。  这是第一个捕获组。|  
|`\s`|与空白字符匹配。|  
|`(?ixn)`|此后，进行不区分大小写的比较，仅进行显式捕获，并忽略正则表达式模式中的空白。|  
|`(?#case-insensitive comparison)`|注释。  它不影响模式匹配行为。|  
|`(d\w+)`|匹配后跟一个或多个字字符的大写或小写“d”。  这是第二个捕获组。|  
|`\b`|与字边界匹配。|  
  
 [!code-csharp[RegularExpressions.Language.Miscellaneous#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.miscellaneous/cs/miscellaneous2.cs#2)]
 [!code-vb[RegularExpressions.Language.Miscellaneous#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.miscellaneous/vb/miscellaneous2.vb#2)]  
  
## 行尾注释  
 数字符号 \(`#`\) 标记 x 模式注释，从正则表达式模式结尾的非转义 \# 字符开始，并继续到行的末尾。  若要使用此构造，必须在实例化 <xref:System.Text.RegularExpressions.Regex> 对象或调用静态 <xref:System.Text.RegularExpressions.Regex> 方法时，启用 `x` 选项（通过内联选项）或向 `option` 参数提供 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> 值。  
  
 下面的示例阐释了行尾注释构造。  它确定字符串是否是一个包含至少一个格式项的复合格式字符串。  下表描述了正则表达式模式中的构造：  
  
 `\{\d+(,-*\d+)*(\:\w{1,4}?)*\}(?x) # Looks for a composite format item.`  
  
|模式|说明|  
|--------|--------|  
|`\{`|匹配左括号。|  
|`\d+`|匹配一个或多个十进制数字。|  
|`(,-*\d+)*`|匹配逗号的零个或一个匹配项，后跟可选负号，负号后跟一个或多个十进制数。|  
|`(\:\w{1,4}?)*`|匹配逗号的零个或一个匹配项，逗号后跟一至四个空白字符，但空白字符尽可能少。|  
|`(?#case insensitive comparison)`|内联注释。  它不影响模式匹配行为。|  
|`\}`|匹配右括号。|  
|`(?x)`|启用忽略模式空白选项，以便识别行尾注释。|  
|`# Looks for a composite format item.`|行尾注释。|  
  
 [!code-csharp[RegularExpressions.Language.Miscellaneous#3](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.miscellaneous/cs/miscellaneous3.cs#3)]
 [!code-vb[RegularExpressions.Language.Miscellaneous#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.miscellaneous/vb/miscellaneous3.vb#3)]  
  
 请注意，不是在正则表达式中提供 `(?x)` 构造，注释可能也可通过调用 <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName> 方法并向其传递 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> 枚举值而被识别。  
  
## 请参阅  
 [正则表达式语言 \- 快速参考](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)