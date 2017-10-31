---
title: "WindowsRuntimeStreamExtensions.AsRandomAccessStream(System.IO.Stream) 方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "System.IO.WindowsRuntimeStreamExtensions.AsRandomAccessStream"
apilocation: 
  - "System.Runtime.WindowsRuntime.dll"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: dcc72283-caed-49ee-b45d-ccaf94e97129
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# WindowsRuntimeStreamExtensions.AsRandomAccessStream(System.IO.Stream) 方法
\[在 .NET Framework 4.5.1 和更高版本中受支持\]  
  
 将指定的流转换为随机访问流。  
  
 **命名空间：** <xref:System.IO?displayProperty=fullName>   
 **程序集：**System.Runtime.WindowsRuntime（在 System.Runtime.WindowsRuntime.dll 中）  
  
## 语法  
  
```csharp  
[CLSCompliantAttribute(false)] public static  IRandomAccessStream AsRandomAccessStream(Stream stream)   
```  
  
```vb  
'Declaration <ExtensionAttribute> _ <CLSCompliantAttribute(False)> _ Public Shared Function AsRandomAccessStream ( _         stream As Stream) As IRandomAccessStream   
```  
  
#### 参数  
 `stream`  
  
 类型：<xref:System.IO.Stream?displayProperty=fullName>   
 要转换的流。  
  
## 返回值  
 类型：[Windows.Storage.Streams.RandomAccessStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.randomaccessstream.aspx)   
 [!INCLUDE[wrt](../../../includes/wrt-md.md)]随机访问流（表示已转换的流）。  
  
## 异常  
  
|例外|条件|  
|--------|--------|  
|<xref:System.NotSupportedException>|要转换的流不支持查找。|  
  
## 备注  
 此扩展方法仅在开发 Windows 应用商店应用时可用。  利用此方法，可以在 Windows 应用商店应用中轻松使用流。  要转换的 .NET Framework 流必须支持查找。  有关更多信息，请参见 <xref:System.IO.Stream.Seek%2A?displayProperty=fullName> 方法。  
  
> [!IMPORTANT]
>  此 API 在 .NET Framework 4.5.1 和更高版本中受支持，但在 4.5 版中不受支持。  
  
## 版本信息  
 **用于 Windows 应用商店应用的 .NET**  
  
 受支持：Windows 8.1  
  
## 请参阅  
 <xref:System.IO.WindowsRuntimeStreamExtensions>   
 [如何：在 .NET Framework 流与 Windows 运行时流之间转换](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md)