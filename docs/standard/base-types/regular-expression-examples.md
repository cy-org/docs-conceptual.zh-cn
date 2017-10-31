---
title: "正则表达式示例 | Microsoft Docs"
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
  - "正则表达式 [.NET Framework]，示例"
  - "正则表达式 [.NET Framework]"
  - "字符串 [.NET Framework]，正则表达式"
ms.assetid: e9fd53f2-ed56-4b09-b2ea-e9bc9d65e6d6
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# 正则表达式示例
本节包含了一些代码示例，用以阐释如何在常见应用程序中使用正则表达式。  
  
> [!NOTE]
>  <xref:System.Web.RegularExpressions> 命名空间包含很多可实现预定义的正则表达式模式来分析 HTML、XML 和 ASP.NET 文档中的字符串的正则表达式对象。  例如，<xref:System.Web.RegularExpressions.TagRegex> 类标识字符串中的开始标记，<xref:System.Web.RegularExpressions.CommentRegex> 类标识字符串中的 ASP.NET 注释。  
  
## 本节内容  
 [示例：扫描 HREF](../../../docs/standard/base-types/regular-expression-example-scanning-for-hrefs.md)  
 提供一个示例，该示例搜索一个输入字符串并输出所有 href\="…" 值及其在字符串中的位置。  
  
 [示例：更改日期格式](../../../docs/standard/base-types/regular-expression-example-changing-date-formats.md)  
 提供一个示例，该示例将 mm\/dd\/yy 格式的日期替换为 dd\-mm\-yy 格式的日期。  
  
 [如何：从 URL 中提取协议和端口号](../../../docs/standard/base-types/how-to-extract-a-protocol-and-port-number-from-a-url.md)  
 提供一个示例，该示例从包含 URL 的字符串中提取协议和端口号。  例如，“http:\/\/www.contoso.com:8080\/letters\/readme.html”将返回“http:8080”。  
  
 [如何：从字符串中剥离无效字符](../../../docs/standard/base-types/how-to-strip-invalid-characters-from-a-string.md)  
 提供一个示例，该示例从字符串中去除无效的非字母数字字符。  
  
 [如何：确认字符串是有效的电子邮件格式](../../../docs/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format.md)  
 提供一个示例，您可用它来验证一个字符串是否是有效的电子邮件格式。  
  
## 参考  
 <xref:System.Text.RegularExpressions>  
 提供 .NET Framework **System.Text.RegularExpressions** 命名空间的类库引用信息。  
  
## 相关章节  
 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)  
 提供正则表达式的编程语言方面的概述。  
  
 [正则表达式对象模型](../../../docs/standard/base-types/the-regular-expression-object-model.md)  
 描述 `System.Text.RegularExpression` 命名空间中包含的正则表达式类，并提供了它们的用法示例。  
  
 [正则表达式行为的详细信息](../../../docs/standard/base-types/details-of-regular-expression-behavior.md)  
 提供有关 .NET Framework 正则表达式的功能和行为的信息。  
  
 [正则表达式语言 \- 快速参考](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)  
 提供有关可用来定义正则表达式的字符集、运算符和构造的信息。