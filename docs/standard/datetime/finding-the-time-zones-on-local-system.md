---
title: "查找在本地系统上定义的时区 | Microsoft Docs"
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
  - "时区标识符 [.NET Framework]"
  - "时区 [.NET Framework], 查找本地系统时区"
  - "时区 [.NET Framework], 本地"
  - "时区 [.NET Framework], 检索"
  - "时区 [.NET Framework], UTC"
  - "UTC 时间, 查找本地系统时区"
ms.assetid: 3f63b1bc-9a4b-4bde-84ea-ab028a80d3e1
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# 查找在本地系统上定义的时区
<xref:System.TimeZoneInfo> 类不公开公共构造函数。  因此，`new` 关键字不能用于创建新的 <xref:System.TimeZoneInfo> 对象。  相反，<xref:System.TimeZoneInfo> 对象通过从注册表检索关于预定义时区的信息或通过创建自定义时区而完成实例化。  本主题讨论从存储在注册表中的数据实例化时区。  此外，<xref:System.TimeZoneInfo> 类的 `static`（Visual Basic 中的 `shared`）属性提供对协调世界时 \(UTC\) 和本地时区的访问。  
  
> [!NOTE]
>  对于在注册表中未定义的时区，可以通过调用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法的重载创建自定义时区。  [如何：创建不带调整规则的时区](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)和[如何：创建带有调整规则的时区](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)主题中讨论了创建自定义时区。  此外，可以通过使用 <xref:System.TimeZoneInfo.FromSerializedString%2A> 方法将 <xref:System.TimeZoneInfo> 对象从序列化字符串还原来对其实例化。  序列化和反序列化 <xref:System.TimeZoneInfo> 对象在 [如何：将时区保存到嵌入的资源中](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)和[如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)主题中讨论。  
  
## 访问独立时区  
 <xref:System.TimeZoneInfo> 类提供两个预定义的时区对象，分别表示 UTC 时间和本地时区。  它们分别可从 <xref:System.TimeZoneInfo.Utc%2A> 和 <xref:System.TimeZoneInfo.Local%2A> 属性获得。  有关访问 UTC 或本地时区的说明，请参阅[如何：访问预定义的 UTC 和本地时区对象](../../../docs/standard/datetime/access-utc-and-local.md)。  
  
 还可以实例化表示注册表中定义的任何时区的 <xref:System.TimeZoneInfo> 对象。  有关实例化特定时区对象的说明，请参阅[如何：实例化 TimeZoneInfo 对象](../../../docs/standard/datetime/instantiate-time-zone-info.md)。  
  
## 时区标识符  
 时区标识符是唯一标识时区的键字段。  虽然大多数键都相对较短，但时区标识符相对较长。  在大多数情况下，其值对应于 <xref:System.TimeZoneInfo.StandardName%2A?displayProperty=fullName> 属性，该属性用于提供时区标准时间的名称。  但是，有例外情况。  确保提供有效标识符最好的办法是枚举系统上可用的时区，并记下其关联的标识符。  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [如何：访问预定义的 UTC 和本地时区对象](../../../docs/standard/datetime/access-utc-and-local.md)   
 [如何：实例化 TimeZoneInfo 对象](../../../docs/standard/datetime/instantiate-time-zone-info.md)   
 [在不同时区之间转换时间](../../../docs/standard/datetime/converting-between-time-zones.md)