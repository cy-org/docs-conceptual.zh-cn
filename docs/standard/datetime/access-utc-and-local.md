---
title: "如何：访问预定义的 UTC 和本地时区对象 | Microsoft Docs"
ms.custom: ""
ms.date: "04/10/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "本地时区访问"
  - "预定义的时区"
  - "时区 [.NET Framework], 本地"
  - "时区 [.NET Framework], 检索"
  - "时区 [.NET Framework], UTC"
  - "UTC 时间, 预定义的"
ms.assetid: 961fb70b-83f0-4dab-a042-cb5fcd817cf5
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：访问预定义的 UTC 和本地时区对象
<xref:System.TimeZoneInfo> 类提供了 <xref:System.TimeZoneInfo.Utc%2A> 和 <xref:System.TimeZoneInfo.Local%2A> 两个属性，这两个属性允许您通过代码访问预定义的时区对象。  本主题讨论如何访问由这两个属性返回的 <xref:System.TimeZoneInfo> 对象。  
  
### 访问协调世界时 \(UTC\) TimeZoneInfo 对象  
  
1.  使用 `static`（在 Visual Basic 中为 `Shared`）<xref:System.TimeZoneInfo.Utc%2A?displayProperty=fullName> 属性访问协调世界时。  
  
2.  不要将该属性返回的 <xref:System.TimeZoneInfo> 对象分配给对象变量，而是继续通过 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=fullName> 属性访问协调世界时。  
  
### 访问本地时区  
  
1.  使用 `static`（在 Visual Basic 中为 `Shared`）<xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> 属性访问本地系统时区。  
  
2.  不要将该属性返回的 <xref:System.TimeZoneInfo> 对象分配给对象变量，而是继续通过 <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> 属性访问本地时区。  
  
## 示例  
 下面的代码使用 <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> 和 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=fullName> 属性转换从美国和加拿大东部标准时区的时间，以及时区名称显示到控制台。  
  
 [!code-csharp[System.TimeZone2.Concepts#13](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#13)]
 [!code-vb[System.TimeZone2.Concepts#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#13)]  
  
 应始终通过 <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> 属性访问本地时区，而不是将本地时区分配给 <xref:System.TimeZoneInfo> 对象变量。  同样，应始终通过 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=fullName> 属性访问协调世界时，而不是将 UTC 时区分配给 <xref:System.TimeZoneInfo> 对象变量。这可以防止 <xref:System.TimeZoneInfo> 对象变量因调用 <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=fullName> 方法而失效。  
  
## 编译代码  
 此示例需要：  
  
-   在项目中添加一个对 System.Core.dll 的引用。  
  
-   使用 `using` 语句导入 <xref:System> 命名空间（在 C\# 代码中需要）。  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [查找在本地系统上定义的时区](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)   
 [如何：实例化 TimeZoneInfo 对象](../../../docs/standard/datetime/instantiate-time-zone-info.md)