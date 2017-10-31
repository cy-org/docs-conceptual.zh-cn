---
title: ".NET Framework 中的类型转换表 | Microsoft Docs"
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
  - "扩大转换"
  - "收缩转换"
  - "类型转换，表"
  - "转换类型，收缩转换"
  - "转换类型，扩大转换"
  - "基类型，转换"
  - "表 [.NET Framework]，类型转换"
  - "数据类型 [.NET Framework]，转换"
ms.assetid: 0ea65c59-85eb-4a52-94ca-c36d3bd13058
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# .NET Framework 中的类型转换表
发生扩大转换。，当一个类型的值转换为相等或更大范围的另一种类型时。  收缩转换时，会发生一个类型的值转换为较小的另一种类型的值时。  本主题中的表阐释了两种转换类型显示的行为。  
  
## 扩大转换  
 下表描述了可以执行，不会丢失信息的扩大转换。  
  
|类型|可以转换，而不会丢失数据|  
|--------|------------------|  
|<xref:System.Byte>|<xref:System.UInt16>, <xref:System.Int16>, <xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.SByte>|<xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int16>|<xref:System.Int32>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.UInt16>|<xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Char>|<xref:System.UInt16>, <xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int32>|<xref:System.Int64>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.UInt32>|<xref:System.Int64>, <xref:System.UInt64>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int64>|<xref:System.Decimal>|  
|<xref:System.UInt64>|<xref:System.Decimal>|  
|<xref:System.Single>|<xref:System.Double>|  
  
 为 <xref:System.Single> 或 <xref:System.Double> 的那些扩大转换可能会导致丢失精度。  下表描述了有时会导致信息丢失的扩大转换。  
  
|类型|可以转换|  
|--------|----------|  
|<xref:System.Int32>|<xref:System.Single>|  
|<xref:System.UInt32>|<xref:System.Single>|  
|<xref:System.Int64>|<xref:System.Single>, <xref:System.Double>|  
|<xref:System.UInt64>|<xref:System.Single>, <xref:System.Double>|  
|<xref:System.Decimal>|<xref:System.Single>, <xref:System.Double>|  
  
## 收缩转换  
 为 <xref:System.Single> 或 <xref:System.Double> 的收缩转换可能导致信息丢失。  如果目标类型无法正确表达源的大小，则结果类型设置为常数 `PositiveInfinity` 或 `NegativeInfinity`。  ，当 <xref:System.Single> 或 <xref:System.Double> 的值超过 `MaxValue` 字段的值时，`PositiveInfinity` 由部件的正数由零和也会返回。  ，当 <xref:System.Single> 或 <xref:System.Double> 的值。 `MinValue` 字段中的值时，会`NegativeInfinity` 产生负数除以零时和也会返回。  从 <xref:System.Double> 的转换到 <xref:System.Single> 可能导致 `PositiveInfinity` 或 `NegativeInfinity`。  
  
 收缩转换可能会导致其他数据类型的信息丢失。  但是， <xref:System.OverflowException> 引发，如果将类型的值不在目标类型的 `MaxValue` 和 `MinValue` 字段指定的范围内，因此，转换在运行时检查确保目标类型的值不超过其 `MaxValue` 或 `MinValue`。  对 <xref:System.Convert?displayProperty=fullName> 类的转换始终以这种方式检查。  
  
 下表列出了 <xref:System.OverflowException> 使用 <xref:System.Convert?displayProperty=fullName> 或所有签出的转换的转换，如果转换的类型的值不在结果类型的定义的大小。  
  
|类型|可以转换|  
|--------|----------|  
|<xref:System.Byte>|<xref:System.SByte>|  
|<xref:System.SByte>|<xref:System.Byte>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64>|  
|<xref:System.Int16>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.UInt16>|  
|<xref:System.UInt16>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>|  
|<xref:System.Int32>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>,<xref:System.UInt32>|  
|<xref:System.UInt32>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>|  
|<xref:System.Int64>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>,<xref:System.UInt32>,<xref:System.UInt64>|  
|<xref:System.UInt64>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>|  
|<xref:System.Decimal>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
|<xref:System.Single>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
|<xref:System.Double>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
  
## 请参阅  
 <xref:System.Convert?displayProperty=fullName>   
 [.NET Framework 中的类型转换](../../../docs/standard/base-types/type-conversion.md)