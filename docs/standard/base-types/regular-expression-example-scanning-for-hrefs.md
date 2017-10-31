---
title: "正则表达式示例：扫描 HREF | Microsoft Docs"
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
  - "用正则表达式进行搜索，示例"
  - "用正则表达式分析文本，示例"
  - "正则表达式，示例"
  - ".NET Framework 正则表达式，示例"
  - "正则表达式 [.NET Framework]，示例"
  - "使用正则表达式进行模式匹配，示例"
ms.assetid: fae2c15b-7adf-4b15-b118-58eb3906994f
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# 正则表达式示例：扫描 HREF
下面的示例搜索输入字符串并显示所有 href\="…" 的值和它们在字符串中的位置。  
  
## Regex 对象  
 由于可以从用户代码多次调用 `DumpHRefs` 方法，因此它会使用 `static`（在 Visual Basic 中为 `Shared`）<xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName> 方法。  这使得正则表达式引擎可以缓存正则表达式，并避免在每次调用该方法时实例化新的 <xref:System.Text.RegularExpressions.Regex> 对象所造成的开销。  随后，将使用一个 <xref:System.Text.RegularExpressions.Match> 对象来循环访问字符串中的所有匹配项。  
  
 [!code-csharp[RegularExpressions.Examples.HREF#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#1)]
 [!code-vb[RegularExpressions.Examples.HREF#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#1)]  
  
 然后，下面的示例演示对 `DumpHRefs` 方法的调用。  
  
 [!code-csharp[RegularExpressions.Examples.HREF#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#2)]
 [!code-vb[RegularExpressions.Examples.HREF#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#2)]  
  
 正则表达式模式 `href\s*=\s*(?:["'](?<1>[^"']*)["']|(?<1>\S+))` 的含义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`href`|匹配文本字符串“href”。  匹配不区分大小写。|  
|`\s*`|匹配零个或多个空白字符。|  
|`=`|匹配等号。|  
|`\s*`|匹配零个或多个空白字符。|  
|`(?:["'](?<1>[^"']*)"&#124;(?<1>\S+))`|匹配下列项之一，但不将结果分配给捕获组：<br /><br /> -   一个引号或单引号，后跟零个或多个引号或单引号以外的任意字符的匹配项，再后跟一个引号或单引号。  按照此模式包含名为 `1` 的组。<br />-   一个或多个非空白字符。  按照此模式包含名为 `1` 的组。|  
|`(?<1>[^"']*)`|将零个或多个引号或单引号以外的任意字符的匹配项分配给名为 `1` 的捕获组。|  
|`"(?<1>\S+)`|将一个或多个非空白字符分配给名为 `1` 的捕获组。|  
  
## 匹配结果类  
 搜索的结果存储在 <xref:System.Text.RegularExpressions.Match> 类中，这提供对该搜索提取的所有子字符串的访问。  因为该类还记忆所搜索的字符串和所使用的正则表达式，所以它还可以调用 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName> 方法来在上一次搜索结束的地方开始另一个搜索。  
  
## 显式命名的捕获  
 在传统的正则表达式中，捕获括号是自动按顺序编号的。  这导致了两个问题。  首先，如果通过插入或移除一组括号修改了一个正则表达式，则必须重写所有引用编号捕获的代码以反映新的编号。  其次，因为不同的括号组经常被用来为可接受的匹配提供两个可替换的表达式，所以可能比较难于确定哪一个可替换的表达式实际返回了结果。  
  
 为解决这些问题，<xref:System.Text.RegularExpressions.Regex> 类支持将匹配捕获到指定槽中的语法`(?<name>…)`（可以用字符串或整数命名槽；但整数可以被更快地回调。）  因此，同一字符串的所有替换匹配都可被定向到同一位置。  如果出现冲突，放置到槽中的最后一个匹配将是成功的匹配。（但是，单个槽的多个匹配的完整列表是可用的。  有关详细信息，请参见 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=fullName> 集合。）  
  
## 请参阅  
 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)