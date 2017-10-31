---
title: "枚举格式字符串 | Microsoft Docs"
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
  - "枚举格式字符串"
  - "格式说明符, 枚举格式字符串"
  - "格式设置 [.NET Framework], 枚举"
ms.assetid: dd1ff672-1052-42cf-8666-4924fb6cd1a1
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 枚举格式字符串
可以使用 <xref:System.Enum.ToString%2A?displayProperty=fullName> 方法创建新的字符串对象，以表示枚举成员的数值、十六进制值或字符串值。  此方法采用某个枚举格式化字符串指定希望返回的值。  
  
 下表列出了枚举格式化字符串及其返回的值。  这些格式说明符不区分大小写。  
  
|格式字符串|结果|  
|-----------|--------|  
|G 或 g|如有可能，将枚举项显示为字符串值，否则显示当前实例的整数值。  如果枚举定义中设置了 **Flags** 特性，则串联每个有效项的字符串值并将各值用逗号分开。  如果未设置 **Flags** 特性，则将无效值显示为数字项。  下面的示例阐释 G 格式说明符。<br /><br /> [!code-csharp[Formatting.Enum#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#1)]
 [!code-vb[Formatting.Enum#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#1)]|  
|F 或 f|如有可能，将枚举项显示为字符串值。  如果值可以完全显示为枚举项的总和（即使未提供 **Flags** 特性），则串联每个有效项的字符串值并将各值用逗号分开。  如果值不能完全由枚举项确定，则将值格式化为整数值。  下面的示例阐释 F 格式说明符。<br /><br /> [!code-csharp[Formatting.Enum#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#2)]
 [!code-vb[Formatting.Enum#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#2)]|  
|D 或 d|以尽可能短的表示形式将枚举项显示为整数值。  下面的示例阐释 D 格式说明符。<br /><br /> [!code-csharp[Formatting.Enum#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#3)]
 [!code-vb[Formatting.Enum#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#3)]|  
|X 或 x|将枚举项显示为十六进制值。  按需要将值表示为带有前导零，以确保值的长度最少有八位。  下面的示例阐释 X 格式说明符。<br /><br /> [!code-csharp[Formatting.Enum#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#4)]
 [!code-vb[Formatting.Enum#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#4)]|  
  
## 示例  
 下面的示例定义一个名为 `Colors` 的枚举，该枚举包含三项：`Red`、`Blue` 和 `Green`。  
  
 [!code-csharp[Formatting.Enum#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#5)]
 [!code-vb[Formatting.Enum#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#5)]  
  
 定义了枚举后，可以按下面的方式声明实例。  
  
 [!code-csharp[Formatting.Enum#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#6)]
 [!code-vb[Formatting.Enum#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#6)]  
  
 随后，`Color.ToString(System.String)` 方法可用于以不同的方式显示枚举值，具体则取决于传递给它的格式说明符。  
  
 [!code-csharp[Formatting.Enum#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#7)]
 [!code-vb[Formatting.Enum#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#7)]  
  
## 请参阅  
 [格式化类型](../../../docs/standard/base-types/formatting-types.md)