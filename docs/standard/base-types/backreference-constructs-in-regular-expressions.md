---
title: "正则表达式中的反向引用构造 | Microsoft Docs"
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
  - ".NET Framework 正则表达式, 反向引用构造"
  - "反向引用"
  - "构造, 反向参照"
  - "正则表达式, 反向引用构造"
ms.assetid: 567a4b8d-0e79-49dc-8df9-f4b1aa376a2a
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 正则表达式中的反向引用构造
反向引用提供了标识字符串中的重复字符或子字符串的方便途径。  例如，如果输入字符串包含某任意子字符串的多个匹配项，则可以使用捕获组匹配第一个出现的子字符串，然后使用反向引用匹配后面出现的子字符串。  
  
> [!NOTE]
>  单独语法用于引用替换字符串中命名的和带编号的捕获组。  有关详细信息，请参阅[替代](../../../docs/standard/base-types/substitutions-in-regular-expressions.md)。  
  
 .NET Framework 定义引用编号和已命名的捕获组的单独语言元素。  有关捕获组的详细信息，请参阅[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)。  
  
## 带编号的后向引用  
 带编号的反向引用使用以下语法：  
  
 `\` *number*  
  
 其中*编号number* 是正则表达式中捕获组的序号位置。  例如，`\4` 匹配第四个捕获组的内容。  如果正则表达式模式中未定义*number*，则将发生分析错误，并且正则表达式引擎将引发<xref:System.ArgumentException>。  例如，正则表达式 `\b(\w+)\s\1` 有效，因为 `(\w+)` 是表达式中的第一个也是唯一一个捕获组。  另一方面，`\b(\w+)\s\2` 无效，并因为没有捕获组编号 `\2` 而引发参数异常。  
  
 请注意八进制转义代码（如 `\16`）和使用相同表示法的 `\`*编号number* 后向引用之间的多义性。  此多义性通过如下方式解决：  
  
-   表达式 `\1` 到 `\9` 总是解释为反向应用，而不是八进制代码。  
  
-   如果多位表达式的第一个数字是 8 或 9（如 `\80` 或 `\91`），则该表达式将被解释为文本。  
  
-   对于编号为 `\10` 或更大值的表达式，如果存在与该编号对应的反向引用，则将该表达式视为反向引用；否则，将这些表达式解释为八进制代码。  
  
-   如果正则表达式包含对未定义的组成员的反向引用，则会发生分析错误,并且正则表达式引擎将引发 <xref:System.ArgumentException>。  
  
 如果有多义性问题，可以使用 `\k<`*名称name*`>` 表示法，该表示法是明确的，并且不会与八进制符号代码混淆。  同样，如 `\xdd` 的十六进制代码是明确的，并且不能与反向引用混淆。  
  
 下面的示例查找字符串中双写的单词字符。  它定义了一个正则表达式 `(\w)\1`，由下列元素组成。  
  
|元素|说明|  
|--------|--------|  
|`(\w)`|匹配字字符，并将其分配给第一捕获组。|  
|`\1`|匹配下一个值与第一捕获组相同的字符。|  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference1.cs#1)]
 [!code-vb[RegularExpressions.Language.Backreferences#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference1.vb#1)]  
  
## 命名的后向引用  
 命名后向引用通过使用下面的语法进行定义：  
  
 `\k<` *name* `>`  
  
 或：  
  
 `\k'` *name* `'`  
  
 *name*是正则表达式模式中定义的捕获组的名字的地方.  如果正则表达式模式中未定义*name*，则将发生分析错误，并且正则表达式引擎将引发<xref:System.ArgumentException>。  
  
 下面的示例查找字符串中双写的单词字符。  它定义了一个正则表达式 `(?<char>\w)\k<char>`，由下列元素组成。  
  
|元素|说明|  
|--------|--------|  
|`(?<char>\w)`|匹配字字符，并将其分配给名为 `char` 的捕获组。|  
|`\k<char>`|匹配下一个值与 `char` 捕获组相同的字符。|  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference2.cs#2)]
 [!code-vb[RegularExpressions.Language.Backreferences#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference2.vb#2)]  
  
 请注意*name*也可以是数字的字符串表示形式。  例如，下面的示例使用正则表达式 `(?<2>\w)\k<2>` 来查找字符串中双写的单词字符。  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#3](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference3.cs#3)]
 [!code-vb[RegularExpressions.Language.Backreferences#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference3.vb#3)]  
  
## 反向引用匹配什么  
 反向引用引用组的最近的定义（当从左到右匹配时，最靠近左侧的定义）。  当组建立多个捕获时，反向引用会引用最近的捕获。  
  
 下面的示例包含正则表达式模式 `(?<1>a)(?<1>\1b)*`，其重新定义命名 \\1 的组。  下表描述了正则表达式中的每个模式。  
  
|模式|说明|  
|--------|--------|  
|`(?<1>a)`|匹配字符“a”，并将结果分配给名为 `1` 的捕获组。|  
|`(?<1>\1b)*`|将命名为 `1` 的组的 0 或 1 匹配项与“b”匹配，并将结果分配给名为 `1` 的捕获的组。|  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#4](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference4.cs#4)]
 [!code-vb[RegularExpressions.Language.Backreferences#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference4.vb#4)]  
  
 在比较正则表达式与输入字符串（“aababb”）时，正则表达式引擎执行下列操作：  
  
1.  它从该字符串的开头开始，并成功匹配"a"与表达式 `(?<1>a)`。  现在 `1` 组的值为 "a"。  
  
2.  它前进至第二个字符，并成功匹配字符串 ab 与表达式 `\1b` 或“ab”。  它将结果“ab”赋给 `\1`。  
  
3.  它前进到第四个字符。  表达式 `(?<1>\1b)` 是要匹配零次或更多次，因此它成功将字符串“abb”与表达式 `\1b` 匹配。  它将“abb”结果赋回给 `\1`。  
  
 在此示例中，`*` 是循环限定符 \-\- 它将重复进行计算，直到正则表达式引擎不能与它所定义的模式匹配时为止。  循环限定符不清除组定义。  
  
 如果一个组尚未捕获任何子字符串，则对该组的反向引用是未定义的并且永远不匹配。  这通过正则表达式模式 `\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b` 说明，其定义如下：  
  
|模式|说明|  
|--------|--------|  
|`\b`|从单词边界开始进行匹配。|  
|`(\p{Lu}{2})`|匹配两个大写字母。  这是第一个捕获组。|  
|`(\d{2})?`|匹配两个十进制数的零个或一个匹配项。  这是第二个捕获组。|  
|`(\p{Lu}{2})`|匹配两个大写字母。  这是第三个捕获组。|  
|`\b`|在单词边界处结束匹配。|  
  
 输入字符串可以匹配此正则表达式，即使由第二个捕获组定义的两个十进制数字不存在。  下面的示例显示了即使匹配成功，仍会在两个成功的捕获组之间找到空的捕获组。  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#5](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference5.cs#5)]
 [!code-vb[RegularExpressions.Language.Backreferences#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference5.vb#5)]  
  
## 请参阅  
 [正则表达式语言 \- 快速参考](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)