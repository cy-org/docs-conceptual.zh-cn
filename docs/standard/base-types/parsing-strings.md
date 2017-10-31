---
title: "在 .NET Framework 中分析字符串 | Microsoft Docs"
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
  - "分析字符串，关于分析字符串"
  - "IFormatProvider 接口，分析字符串"
  - "基类型，分析字符串"
  - "“分析”方法"
  - "分析字符串"
ms.assetid: 5e758b41-db93-456b-8999-99b7304b090d
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 在 .NET Framework 中分析字符串
分析操作可将表示 .NET Framework 基类型的字符串转换为基类型。  例如，分析操作用于将字符串转换为浮点数或日期和时间值。  执行分析操作的最常用方法是 `Parse` 方法。  由于分析是格式设置的反向操作（涉及将基类型转换为字符串表示形式），因此许多相同的规则和约定都适用。  正如格式设置使用实现 <xref:System.IFormatProvider> 接口的对象提供对区域性敏感的格式设置信息一样，分析也使用实现 <xref:System.IFormatProvider> 接口的对象确定如何解释字符串表示形式。  有关更多信息，请参见[格式化类型](../../../docs/standard/base-types/formatting-types.md)。  
  
## 本节内容  
 [分析数值字符串](../../../docs/standard/base-types/parsing-numeric.md)  
 描述如何将字符串转换为 .NET Framework 的 numeric 类型。  
  
 [分析日期和时间字符串](../../../docs/standard/base-types/parsing-datetime.md)  
 描述如何将字符串转换为 .NET Framework 的 **DateTime** 类型。  
  
 [分析其他字符串](../../../docs/standard/base-types/parsing-other.md)  
 描述如何将字符串转换为 **Char**、**Boolean** 和 **Enum** 类型。  
  
## 相关章节  
 [格式化类型](../../../docs/standard/base-types/formatting-types.md)  
 描述一些基本格式设置概念，如格式说明符和格式提供程序。  
  
 [.NET Framework 中的类型转换](../../../docs/standard/base-types/type-conversion.md)  
 描述如何转换类型。  
  
 [基类型](../../../docs/standard/base-types/index.md)  
 描述可执行的与 .NET Framework 基类型相关的常用操作。