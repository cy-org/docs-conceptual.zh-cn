---
title: "在 .NET Framework 中创建新字符串 | Microsoft Docs"
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
  - "Concat 方法"
  - "CopyTo 方法"
  - "Format 方法"
  - "Insert 方法"
  - "Join 方法"
  - "字符串 [.NET Framework], 创建"
ms.assetid: 06fdf123-2fac-4459-8904-eb48ab908a30
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 在 .NET Framework 中创建新字符串
[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 允许通过简单赋值创建字符串，并且还重载类构造函数以支持使用一些不同参数来创建字符串。  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 还在 <xref:System.String?displayProperty=fullName> 类中提供了几个方法，这些方法通过合并多个字符串、字符串数组或对象来创建新的字符串对象。  
  
## 通过赋值创建字符串  
 创建新 <xref:System.String> 对象的最简单方法是将一个字符串赋给 <xref:System.String> 对象。  
  
## 使用类构造函数创建字符串  
 可以使用 <xref:System.String> 类构造函数的重载从字符数组创建字符串。  还可以通过将特定字符重复指定次数来创建新字符串。  
  
## 返回字符串的方法  
 下表列出了返回新字符串对象的几个有用的方法。  
  
|方法名|使用|  
|---------|--------|  
|<xref:System.String.Format%2A?displayProperty=fullName>|从一组输入对象生成格式化的字符串。|  
|<xref:System.String.Concat%2A?displayProperty=fullName>|从两个或多个字符串生成字符串。|  
|<xref:System.String.Join%2A?displayProperty=fullName>|通过合并字符串数组生成新字符串。|  
|<xref:System.String.Insert%2A?displayProperty=fullName>|通过将一个字符串插入到现有字符串的指定索引处生成新的字符串。|  
|<xref:System.String.CopyTo%2A?displayProperty=fullName>|将一个字符串中的指定字符复制到一个字符数组中的指定位置。|  
  
### Format  
 可以使用 **String.Format** 方法来创建格式化字符串和连接表示多个对象的字符串。  此方法自动将传递给它的任何对象转换为字符串。  例如，如果应用程序必须向用户显示 **Int32** 值和 **DateTime** 值，则可以很方便地使用 **Format** 方法来构造表示这些值的字符串。  有关此方法使用的格式化约定的信息，请参见有关[复合格式化](../../../docs/standard/base-types/composite-formatting.md)的章节。  
  
 下面的示例使用 **Format** 方法来创建一个使用整型变量的字符串。  
  
 [!code-csharp[Strings.Creating#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#1)]
 [!code-vb[Strings.Creating#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#1)]  
  
 在此示例中，<xref:System.DateTime.Now%2A?displayProperty=fullName> 按照与当前线程关联的区域性所指定的方式来显示当前日期和时间。  
  
### Concat  
 **String.Concat** 方法可用来方便地从两个或多个现有对象创建新的字符串对象。  它提供了一种不依赖于语言的方法来连接字符串。  该方法接受派生自 **System.Object** 的任何类。  下面的示例会使用两个现有字符串对象和一个分隔符创建一个字符串。  
  
 [!code-csharp[Strings.Creating#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#2)]
 [!code-vb[Strings.Creating#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#2)]  
  
### Join  
 **String.Join** 方法用一个字符串数组和一个分隔符串创建一个新的字符串。  如果希望将多个字符串连接在一起，构成一个可能由逗号分隔的列表，则此方法非常有用。  
  
 下面的示例使用空格来连接一个字符串数组。  
  
 [!code-csharp[Strings.Creating#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#3)]
 [!code-vb[Strings.Creating#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#3)]  
  
### Insert  
 **String.Insert** 方法通过将一个字符串插入到另一个字符串中的指定位置来创建一个新的字符串。  此方法使用从零开始的索引。  下面的示例将一个字符串插入到 `MyString` 的第五个索引位置，并用此值创建一个新字符串。  
  
 [!code-csharp[Strings.Creating#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#4)]
 [!code-vb[Strings.Creating#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#4)]  
  
### CopyTo  
 **String.CopyTo** 方法将字符串的一些部分复制到一个字符数组中。  可以同时指定字符串的开始索引和要复制的字符数。  此方法带有四个参数，即源索引、字符数组、目标索引和要复制的字符数。  所有索引都是从零开始的。  
  
 下面的示例使用 **CopyTo** 方法将单词“Hello”的字符从字符串对象复制到字符数组的第一个索引位置。  
  
 [!code-csharp[Strings.Creating#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#5)]
 [!code-vb[Strings.Creating#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#5)]  
  
## 请参阅  
 [基本字符串操作](../../../docs/standard/base-types/basic-string-operations.md)   
 [复合格式设置](../../../docs/standard/base-types/composite-formatting.md)