---
title: "保存和还原时区 | Microsoft Docs"
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
  - "反序列化 [.NET Framework], 时区"
  - "还原时区"
  - "保存时区"
  - "序列化 [.NET Framework], 时区"
  - "时区对象 [.NET Framework], 反序列化"
  - "时区对象 [.NET Framework], 还原"
  - "时区对象 [.NET Framework], 保存"
  - "时区对象 [.NET Framework], 序列化"
  - "时区 [.NET Framework], 还原"
  - "时区 [.NET Framework], 保存"
ms.assetid: 4028b310-e7ce-49d4-a646-1e83bfaf6f9d
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 保存和还原时区
<xref:System.TimeZoneInfo> 类依赖注册表检索预定义的时区数据。  但是，注册表是一个动态结构。  此外，注册表包含的时区信息主要供操作系统在处理当前年份的时间调整和转换时使用。  对于依赖准确时区数据的应用程序来说，这有两个主要的影响：  
  
-   注册表中可能未定义应用程序需要的时区，或者该时区可能已被重命名或从注册表中移除。  
  
-   注册表中定义的时区可能缺少执行历史时区转换所需的特定调整规则的相关信息。  
  
 <xref:System.TimeZoneInfo> 类支持对时区数据进行序列化（保存）和反序列化（还原），并以此解决了上述限制。  
  
## 时区序列化和反序列化  
 在通过序列化和反序列化时区数据来保存和还原时区时，只需执行两次方法调用：  
  
-   通过调用 <xref:System.TimeZoneInfo> 对象的 <xref:System.TimeZoneInfo.ToSerializedString%2A> 方法可以序列化该对象。  该方法不带任何参数，并会返回一个包含时区信息的字符串。  
  
-   通过向`static` \(`Shared` in Visual Basic\) <xref:System.TimeZoneInfo.FromSerializedString%2A?displayProperty=fullName>方法传递一个序列化字符串，可以从该字符串反序列化 <xref:System.TimeZoneInfo>对象。  
  
## 序列化和反序列化方案  
 这种可将 <xref:System.TimeZoneInfo> 对象保存（或序列化）到一个字符串中以及还原（或反序列化）该对象以供以后使用的能力提高了 <xref:System.TimeZoneInfo> 类的实用性和灵活性。  本节讨论序列化和反序列化最为有用的一些情况。  
  
### 序列化和反序列化应用程序中的时区数据  
 应用程序可以根据需要从字符串还原序列化的时区。  如果从注册表中检索到的时区无法正确转换特定日期范围内的日期和时间，应用程序便可能执行还原操作。  例如，Windows XP 注册表中的时区数据只支持一个调整规则，而 Windows Vista 注册表中定义的时区通常会提供有关两个调整规则的信息。  这意味着，历史时间转换可能是不准确的。  对时区数据执行序列化和反序列化可以应对这种限制。  
  
 在下面的示例中，在引入夏时制之前，不带调整规则的自定义<xref:System.TimeZoneInfo>类定义为表示从1883到 1917的美国东部标准时区。  自定义时区在具有全局范围的变量中序列化。  同时将协调世界时 \(UTC\) 时间传递给时区转换方法 `ConvertUtcTime` 来进行转换。  如果该日期和时间发生在 1917 年或之前，则从一个序列化字符串还原自定义东部标准时区，并由该时区来替换从注册表中检索到的时区。  
  
 [!code-csharp[System.TimeZone2.Serialization.1#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/cs/Serialization.cs#1)]
 [!code-vb[System.TimeZone2.Serialization.1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/vb/Serialization.vb#1)]  
  
### 处理时区异常  
 由于注册表是一个动态结构，因此其内容可能会被无意或有意修改。  这意味着，本应在注册表中定义且应用程序成功执行所必需的时区可能不存在。  如果不支持时区序列化和反序列化，则只能选择处理因结束应用程序而导致的 <xref:System.TimeZoneNotFoundException>。  但是，使用时区序列化和反序列化，可以通过从序列化字符串还原所需的时区来处理意外的 <xref:System.TimeZoneNotFoundException>，从而使应用程序可继续运行。  
  
 下面的示例创建并序列化一个自定义中部标准时区，  然后尝试从注册表中检索该中部标准时区。  如果检索操作引发 <xref:System.TimeZoneNotFoundException> 或 <xref:System.InvalidTimeZoneException>，则异常处理程序将反序列化该时区。  
  
 [!code-csharp[System.TimeZone2.Serialization.2#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/cs/Serialization2.cs#1)]
 [!code-vb[System.TimeZone2.Serialization.2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/vb/Serialization2.vb#1)]  
  
### 根据需要存储和还原序列化字符串  
 上面的示例先将时区信息存储在一个字符串变量中，然后根据需要还原该字符串。  但是，包含序列化时区信息的字符串自身也可以存储在某些存储介质中，例如外部文件、嵌入在应用程序中的资源文件或注册表（请注意，有关自定义时区的信息应与系统的时区注册表项分开存储）。  
  
 按照此方式存储序列化时区字符串还可以将时区创建例程与应用程序本身分开。  例如，时区创建例程可以创建数据文件并在其中包含可供应用程序使用的历史时区信息，然后执行该文件。  这样，该数据文件便可随应用程序一起安装，应用程序在需要时可以打开该数据文件并序列化其中的一个或多个时区。  
  
 有关使用嵌入的资源存储序列化时区数据的示例，请参见[如何：将时区保存到嵌入的资源中](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)和[如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)。  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)