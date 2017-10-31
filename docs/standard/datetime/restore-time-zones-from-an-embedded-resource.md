---
title: "如何：从嵌入的资源还原时区 | Microsoft Docs"
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
  - "时区 [.NET Framework], 反序列化"
  - "时区 [.NET Framework], 还原"
ms.assetid: 6b7b4de9-da07-47e3-8f4c-823f81798ee7
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：从嵌入的资源还原时区
本主题介绍如何还原已保存在资源文件中的时区。  有关保存时区的信息和说明，请参见[如何：将时区保存到嵌入的资源中](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)。  
  
### 从嵌入的资源中反序列化 TimeZoneInfo 对象  
  
1.  如果要检索的时区不是自定义时区，请尝试使用 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 方法将其实例化。  
  
2.  通过传递嵌入的资源文件的完全限定名以及对包含该资源文件的程序集的引用，可以实例化 <xref:System.Resources.ResourceManager> 对象。  
  
     如果无法确定嵌入的资源文件的完全限定名，请使用 [Ildasm.exe（IL 反汇编程序）](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 检查程序集的清单。  清单中的 `.mresource` 项用于标识资源。  在该示例中，资源的完全限定名为 `SerializeTimeZoneData.SerializedTimeZones`。  
  
     如果嵌入资源文件的程序集与包含时区实例化代码的程序集相同，则可以通过调用 `static`（在 Visual Basic 中为 `Shared`）<xref:System.Reflection.Assembly.GetExecutingAssembly%2A> 方法来检索对该资源文件的引用。  
  
3.  如果调用 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 方法失败，或是要实例化自定义时区，请通过调用 <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName> 方法来检索包含该序列化时区的字符串。  
  
4.  通过调用 <xref:System.TimeZoneInfo.FromSerializedString%2A> 方法可反序列化时区数据。  
  
## 示例  
 下面的示例对嵌入的 .NET XML 资源文件中存储的 <xref:System.TimeZoneInfo> 对象执行反序列化。  
  
 [!code-csharp[TimeZone2.Serialization#3](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#3)]
 [!code-vb[TimeZone2.Serialization#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#3)]  
  
 此代码演示如何进行异常处理，以确保存在应用程序所需的 <xref:System.TimeZoneInfo> 对象。  它首先使用 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 方法从注册表中检索 <xref:System.TimeZoneInfo> 对象，从而来尝试实例化该对象。  如果无法实例化时区，该代码则从嵌入的资源文件中检索该时区。  
  
 由于自定义时区（使用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法实例化的时区）的数据并不存储在注册表中，因此该代码并未调用 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 来实例化南极帕默时区，  而是在调用 <xref:System.TimeZoneInfo.FromSerializedString%2A> 方法之前立即检索嵌入的资源文件中包含该时区数据的字符串。  
  
## 编译代码  
 此示例需要：  
  
-   在项目中添加一个对 System.Windows.Forms.dll 和 System.Core.dll 的引用。  
  
-   导入下列命名空间：  
  
     [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
     [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [时区概述](../../../docs/standard/datetime/time-zone-overview.md)   
 [如何：将时区保存到嵌入的资源中](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)