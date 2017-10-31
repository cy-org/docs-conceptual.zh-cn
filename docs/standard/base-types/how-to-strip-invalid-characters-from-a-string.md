---
title: "如何：从字符串中剥离无效字符 | Microsoft Docs"
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
  - "正则表达式，示例"
  - "清理输入"
  - "用户输入，示例"
  - ".NET Framework 正则表达式，示例"
  - "正则表达式 [.NET Framework]，示例"
  - "Regex.Replace 方法"
  - "排除无效字符"
  - "Replace 方法"
  - "验证用户输入"
ms.assetid: b4319c8a-9032-4129-a9d5-6f6fc28e7f32
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：从字符串中剥离无效字符
下面的示例使用静态 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=fullName> 方法从字符串中清除无效字符。  
  
## 示例  
 您可以使用此示例中定义的 `CleanInput` 方法，清除掉在接受用户输入的文本字段中输入的可能有害的字符。  在这种情况下，`CleanInput` 会清除掉除句点 \(.\)、@ 符号和连字符 \(\-\) 以外的其他所有非字母数字字符并返回剩余字符串。  但是，您可以修改正则表达式模式，以使其能够清除不应包括在输入字符串中的任何字符。  
  
 [!code-csharp[RegularExpressions.Examples.StripChars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.StripChars/cs/Example.cs#1)]
 [!code-vb[RegularExpressions.Examples.StripChars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.StripChars/vb/Example.vb#1)]  
  
 正则表达式模式 `[^\w\.@-]` 匹配除单词字符、句点、@ 符号或连字符之外的任何字符。  单词字符是任何字母、十进制数字或标点连接符（如下划线）。  与此模式匹配的任何字符都将替换为由替换模式定义的字符串 <xref:System.String.Empty?displayProperty=fullName>。  若要在用户输入中允许使用其他字符，请在正则表达式模式中将这些字符添加到字符类中。  例如，正则表达式模式 `[^\w\.@-\\%]` 还允许在输入字符串中使用百分号和反斜杠。  
  
## 请参阅  
 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)