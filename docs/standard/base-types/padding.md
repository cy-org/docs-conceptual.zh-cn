---
title: "在 .NET Framework 中填充字符串 | Microsoft Docs"
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
  - "填充字符串"
  - "PadLeft 方法"
  - "PadRight 方法"
  - "字符串 [.NET Framework], 填充"
  - "空白"
ms.assetid: 84a9f142-3244-4c90-ba02-21af9bbaff71
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 在 .NET Framework 中填充字符串
使用下列 <xref:System.String> 方法之一创建新的字符串，其中包含原始字符串以及用于填充原始字符串使其达到指定总长度的前导或尾随字符。  填充字符可以是空格或指定字符，因此可显示为右对齐或左对齐。  
  
|方法名|使用|  
|---------|--------|  
|<xref:System.String.PadLeft%2A?displayProperty=fullName>|用前导字符填充字符串使其达到指定的总长度。|  
|<xref:System.String.PadRight%2A?displayProperty=fullName>|用尾随字符填充字符串使其达到指定的总长度。|  
  
## PadLeft  
 <xref:System.String.PadLeft%2A?displayProperty=fullName> 方法创建新的字符串，将足够的前导填充字符连接到原始字符串使其达到指定的总长度。  <xref:System.String.PadLeft%28System.Int32%29?displayProperty=fullName> 方法使用空白作为填充字符，而且使用 <xref:System.String.PadLeft%28System.Int32%2CSystem.Char%29?displayProperty=fullName> 方法可以指定自己的填充字符。  
  
 下面的代码示例使用 <xref:System.String.PadLeft%2A> 方法创建长度为 20 个字符的新字符串。  该示例向控制台显示“`--------Hello World!`”。  
  
 [!code-cpp[Conceptual.String.BasicOps#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#3)]
 [!code-csharp[Conceptual.String.BasicOps#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#3)]
 [!code-vb[Conceptual.String.BasicOps#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#3)]  
  
## PadRight  
 <xref:System.String.PadRight%2A?displayProperty=fullName> 方法创建新的字符串，将足够的尾随填充字符连接到原始字符串使其达到指定的总长度。  <xref:System.String.PadRight%28System.Int32%29?displayProperty=fullName> 方法使用空白作为填充字符，而且使用 <xref:System.String.PadRight%28System.Int32%2CSystem.Char%29?displayProperty=fullName> 方法可以指定自己的填充字符。  
  
 下面的代码示例使用 <xref:System.String.PadRight%2A> 方法创建一个长度为二十个字符的新字符串。  该示例将“`Hello World!--------`”显示到控制台。  
  
 [!code-cpp[Conceptual.String.BasicOps#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#4)]
 [!code-csharp[Conceptual.String.BasicOps#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#4)]
 [!code-vb[Conceptual.String.BasicOps#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#4)]  
  
## 请参阅  
 [基本字符串操作](../../../docs/standard/base-types/basic-string-operations.md)