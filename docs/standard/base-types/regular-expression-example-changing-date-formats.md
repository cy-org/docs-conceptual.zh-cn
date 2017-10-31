---
title: "正则表达式示例：更改日期格式 | Microsoft Docs"
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
ms.assetid: 5fcc75a5-09d7-45ae-a4c0-9ad6085ac83d
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# 正则表达式示例：更改日期格式
下面的代码示例使用<xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=fullName>方法来替换时间，该时间以用*dd*\-*mm*\-*yy*格式的*mm*\/*dd*\/*yy*为格式。  
  
## 示例  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#1)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#1)]  
  
 下面的代码演示如何在应用程序中调用 `MDYToDMY` 方法。  
  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#2)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#2)]  
  
## 注释  
 正则表达式模式 `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` 的含义如下表所示。  
  
|模式|说明|  
|--------|--------|  
|`\b`|在单词边界处开始匹配。|  
|`(?<month>\d{1,2})`|匹配一个或两个十进制数字。  这是 `month` 捕获组。|  
|`/`|匹配左斜线。|  
|`(?<day>\d{1,2})`|匹配一个或两个十进制数字。  这是 `day` 捕获的组。|  
|`/`|匹配左斜线。|  
|`(?<year>\d{2,4})`|匹配两个到四个十进制数。  这是 `year` 捕获的组。|  
|`\b`|在单词边界处结束匹配。|  
  
 模式 `${day}-${month}-${year}` 如下表所示定义了替换字符串。  
  
|模式|说明|  
|--------|--------|  
|`$(day)`|添加由 `day` 捕获组捕获的字符串。|  
|`-`|添加连字符。|  
|`$(month)`|添加由 `month` 捕获组捕获的字符串。|  
|`-`|添加连字符。|  
|`$(year)`|添加由 `year` 捕获组捕获的字符串。|  
  
## 请参阅  
 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)