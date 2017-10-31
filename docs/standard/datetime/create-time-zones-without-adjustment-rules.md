---
title: "如何：创建不带调整规则的时区 | Microsoft Docs"
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
  - "调整规则 [.NET Framework]"
  - "时区 [.NET Framework], 调整规则"
  - "时区 [.NET Framework], 创建"
ms.assetid: a6af8647-7893-4f29-95a9-d94c65a6e8dd
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：创建不带调整规则的时区
在特定的系统上，应用程序需要的精确时区信息可能不存在，这有多种原因：  
  
-   本地系统的注册表中从未定义该时区。  
  
-   有关该时区的数据已被修改或已从注册表中移除。  
  
-   该时区存在，但它不具有与特定历史时期的时区调整有关的信息。  
  
 在这些情况下，可以调用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法定义应用程序所需的时区。  您可以使用此方法的重载创建带有或不带调整规则的时区。  如果该时区支持夏时制，则可以用固定调整规则或浮动调整规则来定义调整方式（有关这些术语的定义，请参见[时区概述](../../../docs/standard/datetime/time-zone-overview.md)中的“时区术语”一节）。  
  
> [!IMPORTANT]
>  通过调用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法创建的自定义时区不会被添加到注册表中。  它们只能通过由 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法调用返回的对象引用进行访问。  
  
 本主题介绍如何创建不带调整规则的时区。  若要创建支持夏时制调整规则的时区，请参见[如何：创建带有调整规则的时区](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)。  
  
### 创建不带调整规则的时区  
  
1.  定义时区的显示名称。  
  
     显示名称应遵循相对标准的格式，其中时区的协调世界时 \(UTC\) 偏移量用括号括起来，后面是一个字符串，用于标识时区、该时区中的一个或多个城市或者该时区中的一个或多个国家\/地区。  
  
2.  定义时区的标准时间名称。  此字符串通常还用作时区的标识符。  
  
3.  如果要使用不同于时区标准名称的标识符，请定义时区标识符。  
  
4.  实例化定义时区的 UTC 偏移量的 <xref:System.TimeSpan> 对象。  时间晚于 UTC 的时区有正偏移值。  时间早于 UTC 的时区有负偏移值。  
  
5.  调用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%29?displayProperty=fullName> 方法可实例化新时区。  
  
## 示例  
 下面的示例定义了一个南极莫森自定义时区，此时区不带调整规则。  
  
 [!code-csharp[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#1)]
 [!code-vb[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#1)]  
  
 分配给 <xref:System.TimeZoneInfo.DisplayName%2A> 属性的字符串遵循一种标准格式，其中先是时区的 UTC 偏移量，后面跟有该时区的友好说明。  
  
## 编译代码  
 此示例需要：  
  
-   在项目中添加一个对 System.Core.dll 的引用。  
  
-   导入下列命名空间：  
  
     [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
     [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [时区概述](../../../docs/standard/datetime/time-zone-overview.md)   
 [如何：创建带有调整规则的时区](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)