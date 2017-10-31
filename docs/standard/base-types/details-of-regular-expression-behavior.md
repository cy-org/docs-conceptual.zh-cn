---
title: "正则表达式行为的详细信息 | Microsoft Docs"
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
  - "正则表达式，行为"
  - ".NET Framework 正则表达式，行为"
ms.assetid: 0ee1a6b8-caac-41d2-917f-d35570021b10
caps.latest.revision: 27
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 27
---
# 正则表达式行为的详细信息
.NET Framework 正则表达式引擎是回溯的正则表达式匹配器，它并入了传统的非确定性有限自动机 \(NFA\) 引擎（例如 Perl、Python、Emacs 和 Tcl 使用的引擎）。  这使其有别于更快的、但功能更有限的纯正则表达式确定性有限自动机 \(DFA\) 引擎，例如在 awk、egrep 或 lex 中提供的那些引擎。  这也使其有别于标准化的、但较慢的 POSIX NFA。  下面的章节介绍正则表达式引擎的三种类型，并说明为什么要在 .NET Framework 中使用传统的 NFA 引擎来实现正则表达式。  
  
## NFA 引擎的优点  
 当 DFA 引擎执行模式匹配时，其处理顺序由输入字符串驱动。  此引擎从输入字符串的开头开始，依次按顺序逐个字符进行比对，以确定下一个字符是否与正则表达式模式相匹配。  DFA 引擎可以确保匹配可能的最长的字符串。  由于 DFA 引擎永远不测试相同的字符两次，因此它们不支持回溯。  但是，因为 DFA 引擎只包含有限的状态，所以它不能匹配具有反向引用的模式；并且因为它不构造显式扩展，所以它不可以捕获子表达式。  
  
 与 DFA 引擎不同，当传统的 NFA 引擎执行模式匹配时，其处理顺序由正则表达式模式驱动。  此引擎在处理特定的语言元素时将使用贪婪匹配；也就是说，它将尽可能多地匹配输入字符串。  不过，它也会在成功匹配子表达式后保存其状态。  如果匹配最终失败，则此引擎可返回到保存的状态以便能尝试其他匹配。  放弃成功的子表达式匹配以便正则表达式中后面的语言元素也能匹配的处理过程称作“回溯”。  NFA 引擎使用回溯来按特定顺序测试正则表达式的所有可能的扩展，并接受第一个匹配项。  因为传统的 NFA 引擎会为成功的匹配构造正则表达式的特定扩展，所以它可以捕获子表达式匹配和匹配的反向引用。  但是，由于传统的 NFA 回溯，它可以多次访问相同的状态（如果它通过不同的路径到达该状态）。  因此，在最坏情况下，它的执行速度可能非常慢。  因为传统的 NFA 引擎接受它找到的第一个匹配项，所以它还可能会导致其他（可能更长）匹配项未被发现。  
  
 POSIX NFA 引擎与传统的 NFA 引擎类似，不同的一点在于：在它们可以确保已找到了可能的最长的匹配之前，它们将继续回溯。  因此，POSIX NFA 引擎的速度慢于传统的 NFA 引擎；并且在使用 POSIX NFA 引擎时，您恐怕不会愿意在更改回溯搜索的顺序的情况下来支持较短的匹配搜索，而非较长的匹配搜索。  
  
 程序员更为喜欢传统的 NFA 引擎的原因在于，它们可以比 DFA 引擎或 POSIX NFA 引擎提供对字符串匹配的更多控制。  尽管在最坏情况下 NFA 引擎的运行速度稍慢，但您可以通过使用降低多义性和限制回溯的模式，控制这些引擎以在线性时或多项式时状态下查找匹配项。  换句话说，虽然 NFA 引擎是以牺牲性能的代价来换取功能和灵活性的，但大多数情况下，只要正则表达式编写合理，避免出现因回溯导致性能呈指数级降低的情况，它们提供的性能还是比较好，至少是可接受的。  
  
> [!NOTE]
>  有关过多使用回溯对性能造成的负面影响以及通过编写正则表达式来解决这些问题的方法的信息，请参见[回溯](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)。  
  
## .NET Framework 引擎功能  
 为了利用传统 NFA 引擎的优点，.NET Framework 正则表达式引擎包括了一组完整的构造，使程序员能够操纵回溯引擎。  这些构造可被用于更快地找到匹配，或支持特定扩展，而非其他扩展。  
  
 .NET Framework 正则表达式引擎的其他功能包括：  
  
-   懒惰的数量词: `??`, `*?`, `+?`, `{`*n*`,`*m*`}?`。  这些构造指示回溯引擎首先搜索最少数目的重复。  与之相反，普通的“贪婪的”限定符首先尝试匹配最大数目的重复。  下面的示例对二者之间的差异进行说明。  正则表达式匹配以某个数字结束的句子，而捕获组用于提取该数字。  正则表达式 `.+(\d+)\.` 包含贪婪限定符 `.+`，这使正则表达式引擎仅捕获该数字的最后一位数。  相比之下，正则表达式 `.+?(\d+)\.` 包含惰性限定符 `.+?`，这使正则表达式引擎捕获整个数字。  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lazy1.cs#1)]
     [!code-vb[Conceptual.RegularExpressions.Design#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lazy1.vb#1)]  
  
     此正则表达式的贪婪版本和惰性版本的定义如下表所示。  
  
    |模式|说明|  
    |--------|--------|  
    |`.+`（贪婪限定符）|匹配任意字符的至少一个匹配项。  这会使正则表达式引擎先匹配整个字符串，然后根据需要进行回溯以匹配模式的其余部分。|  
    |`.+?`（惰性限定符）|匹配任意字符的至少一个匹配项（但尽可能少地匹配）。|  
    |`(\d+)`|匹配至少一个数字字符，并将其分配给第一个捕获组。|  
    |`\.`|匹配句点。|  
  
     有关惰性限定符的更多信息，请参见[数量词](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md)。  
  
-   正预测先行： `(?=`*subexpression*`)`。  此功能允许回溯引擎在匹配子表达式后返回到文本中相同的作用点。  这对于通过验证起始于相同位置的多个模式来搜索整个文本是很有用的。  它还允许引擎验证匹配的结尾是否存在某个子字符串，而无需在匹配的文本中包含该子字符串。  下面的示例使用正预测先行从句子中提取未后跟标点符号的单词。  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookahead1.cs#2)]
     [!code-vb[Conceptual.RegularExpressions.Design#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookahead1.vb#2)]  
  
     正则表达式 `\b[A-Z]+\b(?=\P{P})` 的定义如下表所示。  
  
    |模式|说明|  
    |--------|--------|  
    |`\b`|在单词边界处开始匹配。|  
    |`[A-Z]+`|与任意字母字符匹配一次或多次。  由于 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName> 方法是利用 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> 选项来调用的，因此比较不区分大小写。|  
    |`\b`|在单词边界处结束匹配。|  
    |`(?=\P{P})`|查看前一个字符来确定下一个字符是否为标点符号。  如果不是，则表明匹配成功。|  
  
     有关正预测先行断言的更多信息，请参见[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)。  
  
-   负预测先行： `(?!`*subexpression*`)`。  此功能增加了只在子表达式匹配失败的情况下才匹配表达式的能力。  这对于删改一个搜索特别有用，因为提供应被排除的情况的表达式通常比提供必须被包括在内的情况的表达式要简单一些。  例如，编写搜索不以“non”起始的单词的表达式就很困难。  下面的示例使用负预测先行来排除它们。  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookahead2.cs#3)]
     [!code-vb[Conceptual.RegularExpressions.Design#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookahead2.vb#3)]  
  
     正则表达式模式 `\b(?!non)\w+\b` 的定义如下表所示。  
  
    |模式|说明|  
    |--------|--------|  
    |`\b`|在单词边界处开始匹配。|  
    |`(?!non)`|查看前一个字符以确保当前字符串不以“non”开始。  如果当前字符串以“non”开始，则表明匹配失败。|  
    |`(\w+)`|匹配一个或多个单词字符。|  
    |`\b`|在单词边界处结束匹配。|  
  
     有关负预测先行断言的更多信息，请参见[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)。  
  
-   条件计算：`(?(`*expression*`)`*yes* `|` *no* `)` 和 `(?(`*name*`)`*yes* `|` *no* `)`，其中*expression*是要匹配的子表达式，*name* 是捕获组的名称；*yes* 是当找到 *expression*的匹配项或*name*是有效的非空捕获组时要匹配的字符串；而 *no*是当未找到*expression* 的匹配项或*name* 是无效时的子表达式，非空捕获组。  此功能允许引擎根据前面的子表达式匹配的结果或零宽度断言的结果，使用多个替换模式进行搜索。  这提供了超越反向引用所允许的、更为强大的功能，例如，基于是否已匹配上一个子表达式来匹配子表达式。  下面的示例中的正则表达式匹配供公用和内部使用的段落。  仅供内部使用的段落以 `<PRIVATE>` 标记开始。  正则表达式模式 `^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$` 使用条件计算向单独的捕获组分配公用和内部使用的段落内容。  然后可以按不同方式处理这些段落。  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/conditional1.cs#4)]
     [!code-vb[Conceptual.RegularExpressions.Design#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/conditional1.vb#4)]  
  
     正则表达式模式的定义如下表所示。  
  
    |模式|说明|  
    |--------|--------|  
    |`^`|从行的开头开始匹配。|  
    |`(?<Pvt>\<PRIVATE\>\s)?`|匹配后跟空格字符的字符串 `<PRIVATE>` 的零个或一个匹配项。  将匹配项分配给名为 `Pvt` 的捕获组。|  
    |`(?(Pvt)((\w+\p{P}?\s)+)`|如果 `Pvt` 捕获组存在，则匹配一个或多个以下模式：一个或多个单词字符，后跟零个或一个标点分隔符，再后跟一个空格字符。  将子字符串分配给第一个捕获组。|  
    |`&#124;((\w+\p{P}?\s)+))`|如果 `Pvt` 捕获组不存在，则匹配一个或多个以下模式：一个或多个单词字符，后跟零个或一个标点分隔符，再后跟一个空格字符。  将子字符串分配给第三个捕获组。|  
    |`\r?$`|匹配行尾或字符串的结尾。|  
  
     有关条件计算的更多信息，请参见[备用构造](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md)。  
  
-   平衡组定义: `(?<`*name1*`-`*name2*`>` *subexpression*`)`。  此功能允许正则表达式引擎跟踪嵌套构造，如圆括号或左括号和右括号。  有关示例，请参见[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)。  
  
-   非回溯子表达式（也称作贪婪子表达式）：`(?>`*subexpression*`)`。  此功能允许回溯引擎确保子表达式只匹配为该子表达式找到的第一个匹配项，就好像该表达式独立于其包含的表达式运行。  如果不使用此构造，则来自更大的表达式的回溯搜索可能会更改子表达式的行为。  例如，正则表达式 `(a+)\w` 将匹配一个或多个“a”字符，以及跟在“a”字符序列后的一个单词字符，并将“a”字符序列分配给第一个捕获组，但如果输入字符串的最后一个字符也是“a”，则由 `\w` 语言元素匹配“a”字符序列且该序列不会包含在捕获组中。  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/nonbacktracking2.cs#7)]
     [!code-vb[Conceptual.RegularExpressions.Design#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/nonbacktracking2.vb#7)]  
  
     正则表达式 `((?>a+))\w` 将阻止此行为。  由于匹配所有连续的“a”字符时未使用回溯，因此第一个捕获组将包含所有连续的“a”字符。  如果“a”字符后面未跟有至少一个“a”字符之外的其他字符，则表明匹配失败。  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/nonbacktracking1.cs#8)]
     [!code-vb[Conceptual.RegularExpressions.Design#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/nonbacktracking1.vb#8)]  
  
     有关非回溯子表达式的更多信息，请参见[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)。  
  
-   从右到左匹配，此功能是通过将 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> 选项提供给 <xref:System.Text.RegularExpressions.Regex> 类构造函数或静态实例匹配方法来指定的。  此功能在从右到左而非从左到右搜索的情况下十分有用，或者在从模式的右侧部分（而非左侧部分）开始匹配更为有效的情况下十分有用。  如下面的示例所示，使用从右到左匹配可以更改贪婪限定符的行为。  该示例对以数字结束的句子执行两次搜索。  使用贪婪限定符 `+` 的从左到右搜索将匹配句子中的六位数字之一，而从右到左搜索将匹配所有六位数字。  有关正则表达式模式的说明，请参见本节中先前阐释惰性限定符的示例。  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/rtl1.cs#6)]
     [!code-vb[Conceptual.RegularExpressions.Design#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/rtl1.vb#6)]  
  
     有关从右到左匹配的更多信息，请参见[正则表达式选项](../../../docs/standard/base-types/regular-expression-options.md)。  
  
-   正回顾和负回顾：正回顾的 `(?<=`*subexpression*`)` 和负回顾的 `(?<!`*subexpression*`)`。  此功能与本主题中之前讨论的预测先行类似。  因为正则表达式引擎允许完全的从右到左匹配，所以正则表达式允许无限制的回顾。  此外，还可以使用正回顾和负回顾在嵌套子表达式为外部表达式的超集时避免嵌套限定符。  具有此类嵌套限定符的正则表达式通常性能较差。  例如，下面的示例验证一个字符串是否以字母数字字符开头和结尾，并验证该字符串中的任何其他字符是否为某个更大的子集之一。  它构成了用于验证电子邮件地址的正则表达式的一部分；有关更多信息，请参见[如何：确认字符串是有效的电子邮件格式](../../../docs/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format.md)。  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookbehind1.cs#5)]
     [!code-vb[Conceptual.RegularExpressions.Design#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookbehind1.vb#5)]  
  
     正则表达式 `^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$` 的定义如下表所示。  
  
    |模式|说明|  
    |--------|--------|  
    |`^`|从字符串的开头开始匹配。|  
    |`[A-Z0-9]`|匹配任意数字或字母数字字符。（比较不区分大小写。）|  
    |`([-!#$%&'.*+/=?^`{}&#124;~\w])*`|匹配零个或多个任意单词字符或下列任意字符： \-, \!, \#, $, %, &, ', ., \*, \+, \/, \=, ?, ^, \`, {, }, &#124;, 或 ~。|  
    |`(?<=[A-Z0-9])`|后向查看前一个字符，该字符必须是数字或字母数字字符。（比较不区分大小写。）|  
    |`$`|在字符串的结尾结束匹配。|  
  
     有关正回顾和负回顾的更多信息，请参见[分组构造](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)。  
  
## 相关主题  
  
|标题|说明|  
|--------|--------|  
|[回溯](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)|提供关于正则表达式回溯如何分支以查找替换的匹配方面的信息。|  
|[编译和重复使用](../../../docs/standard/base-types/compilation-and-reuse-in-regular-expressions.md)|提供关于如何编译和重复使用正则表达式以提高性能方面的信息。|  
|[线程安全](../../../docs/standard/base-types/thread-safety-in-regular-expressions.md)|提供有关正则表达式线程安全的信息，并说明应在何时同步对正则表达式对象的访问。|  
|[.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)|提供正则表达式的编程语言方面的概述。|  
|[正则表达式对象模型](../../../docs/standard/base-types/the-regular-expression-object-model.md)|提供阐释如何使用正则表达式类的信息和代码示例。|  
|[正则表达式示例](../../../docs/standard/base-types/regular-expression-examples.md)|包含阐释如何在常见的应用程序中使用正则表达式的代码示例。|  
|[正则表达式语言 \- 快速参考](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)|提供有关可用来定义正则表达式的字符集、运算符和构造的信息。|  
  
## 引用  
 <xref:System.Text.RegularExpressions?displayProperty=fullName>