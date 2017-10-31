---
title: "如何：将时区保存到嵌入的资源中 | Microsoft Docs"
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
  - "时区对象 [.NET Framework], 保存"
  - "时区对象 [.NET Framework], 序列化"
  - "时区 [.NET Framework], 保存"
ms.assetid: 3c96d83a-a057-4496-abb0-8f4b12712558
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：将时区保存到嵌入的资源中
时区识别应用程序通常要求存在某个特定的时区。  但是，由于各个 <xref:System.TimeZoneInfo> 对象的可用性取决于本地系统的注册表中存储的信息，因此即使是通常可用的时区也可能不存在。  此外，对于使用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法实例化的自定义时区，其相关信息在注册表中并不与其他时区信息存储在一起。  若要确保可在需要时获得这些时区，可以通过序列化来保存它们，以后再通过反序列化来还原它们。  
  
 通常，序列化 <xref:System.TimeZoneInfo> 对象的过程在时区识别应用程序之外单独进行。  根据用于保存序列化 <xref:System.TimeZoneInfo> 对象的数据存储区，可以将时区数据序列化为设置或安装例程的一部分（例如，当数据存储在注册表的应用程序键中时），或将其序列化为在编译最终应用程序之前运行的实用工具例程的一部分（例如，当序列化数据存储在 .NET XML 资源 \(.resx\) 文件中时）。  
  
 除了与应用程序一起编译的资源文件外，还有其他一些数据存储区可用于保存时区信息。  这些要求包括：  
  
-   注册表。  请注意，应用程序应使用自己应用程序键的子项来存储自定义时区数据，而不应使用 HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Time Zones 的子项。  
  
-   配置文件。  
  
-   其他系统文件。  
  
### 通过将时区序列化到 .resx 文件中来保存时区  
  
1.  检索一个现有的时区或创建一个新时区。  
  
     若要检索现有的时区，请参见[如何：访问预定义的 UTC 和本地时区对象](../../../docs/standard/datetime/access-utc-and-local.md)和[如何：实例化 TimeZoneInfo 对象](../../../docs/standard/datetime/instantiate-time-zone-info.md)。  
  
     若要创建新时区，请调用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法的重载之一。  有关更多信息，请参见[如何：创建不带调整规则的时区](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)和[如何：创建带有调整规则的时区](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)。  
  
2.  调用 <xref:System.TimeZoneInfo.ToSerializedString%2A> 方法，以创建包含时区数据的字符串。  
  
3.  通过向 <xref:System.IO.StreamWriter> 类构造函数提供 .resx 文件的名称和路径（可选）来实例化 <xref:System.IO.StreamWriter> 对象。  
  
4.  通过将 <xref:System.IO.StreamWriter> 对象传递给 <xref:System.Resources.ResXResourceWriter> 类构造函数来实例化 <xref:System.Resources.ResXResourceWriter> 对象。  
  
5.  将时区的序列化字符串传递给 <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=fullName> 方法。  
  
6.  调用 <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=fullName> 方法。  
  
7.  调用 <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=fullName> 方法。  
  
8.  通过调用 <xref:System.IO.StreamWriter> 对象的 <xref:System.IO.StreamWriter.Close%2A> 方法来关闭该对象。  
  
9. 将生成的 .resx 文件添加到应用程序的 Visual Studio 项目中。  
  
10. 使用 Visual Studio 中的**“属性”**窗口，确保 .resx 文件的**“生成操作”**属性已设置为**“嵌入的资源”**。  
  
## 示例  
 下面的示例将一个表示中部标准时间的 <xref:System.TimeZoneInfo> 对象以及一个表示南极帕默站时间的 <xref:System.TimeZoneInfo> 对象序列化到一个名为 SerializedTimeZones.resx 的 .NET XML 资源文件中。  中部标准时间通常在注册表中定义，而南极帕默站则是一个自定义时区。  
  
 [!code-csharp[TimeZone2.Serialization#1](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#1)]
 [!code-vb[TimeZone2.Serialization#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#1)]  
  
 此示例序列化了 <xref:System.TimeZoneInfo> 对象，这样便可在编译时从资源文件中获得它们。  
  
 由于 <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=fullName> 方法向 .NET XML 资源文件中添加了完整的头信息，因此无法将其用于向现有文件添加资源。  为了处理这一问题，该示例会检查 SerializedTimeZones.resx 文件，如果该文件存在，则将其所有资源（两个序列化的时区除外）存储在泛型 <xref:System.Collections.Generic.Dictionary%602> 对象中。  随后，该示例会删除现有文件，并将现有资源添加到新的 SerializedTimeZones.resx 文件中。  序列化的时区数据也会被添加到此文件中。  
  
 资源的键（或**“名称”**）字段不应包含嵌入的空格。  在将时区标识符分配给资源文件之前，应调用 <xref:System.String.Replace%28System.String%2CSystem.String%29> 方法移除时区标识符中嵌入的所有空格。  
  
## 编译代码  
 此示例需要：  
  
-   在项目中添加一个对 System.Windows.Forms.dll 和 System.Core.dll 的引用。  
  
-   导入下列命名空间：  
  
     [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
     [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [时区概述](../../../docs/standard/datetime/time-zone-overview.md)   
 [如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)