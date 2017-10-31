---
title: "如何：从 URL 中提取协议和端口号 | Microsoft Docs"
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
  - ".NET Framework 正则表达式, 示例"
  - "分析带有正则表达式的文本, 示例"
  - "正则表达式的模式匹配, 示例"
  - "正则表达式 [.NET Framework], 示例"
  - "正则表达式, 示例"
  - "用正则表达式搜索, 示例"
ms.assetid: ab7f62b3-6d2c-4efb-8ac6-28600df5fd5c
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：从 URL 中提取协议和端口号
下面的示例从 URL 中提取协议和端口号。  
  
## 示例  
 该示例使用 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=fullName> 方法返回后跟冒号再跟端口号的协议。  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/Example.cs#1)]
 [!code-vb[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/Example.vb#1)]  
  
 正则表达式模式 `^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/` 可以解释为下表中所示的那样。  
  
|模式|说明|  
|--------|--------|  
|`^`|从字符串的开头部分开始匹配。|  
|`(?<proto>\w+)`|匹配一个或多个单词字符。  将此组命名为 `proto`。|  
|`://`|匹配冒号后跟两个左斜线的形式。|  
|`[^/]+?`|匹配左斜线之外的任何字符的一个或多个匹配项（但要尽可能少）。|  
|`(?<port>:\d+)?`|匹配零个或一个以冒号后跟一个或多个数字字符形式存在的匹配项。  将此组命名为 `port`。|  
|`/`|匹配左斜线。|  
  
 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=fullName> 方法扩展 `${proto}${port}` 替换序列，该序列用于连接在正则表达式模式中捕获的两个命名组的值。  它是显式串联从 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=fullName> 属性返回的集合对象中检索的字符串的一种简便的替代方法。  
  
 本示例使用带有两个替换项（`${proto}` 和 `${port}`）的 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=fullName> 方法以在输出字符串中包括捕获的组。  您可以改为从匹配的 <xref:System.Text.RegularExpressions.GroupCollection> 对象中检索捕获的组，如以下代码所示。  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/example2.cs#2)]
 [!code-vb[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/example2.vb#2)]  
  
## 请参阅  
 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)