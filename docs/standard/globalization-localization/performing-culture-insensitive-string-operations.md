---
title: "执行不区分区域性的字符串操作 | Microsoft Docs"
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
  - "大小写映射"
  - "自定义大小写映射"
  - "区域性，自定义排序规则"
  - "自定义排序规则"
  - "不区分区域性的字符串操作，用于执行的选项"
  - "区域性，自定义大小写映射"
  - "不区分区域性的字符串操作，方法重载"
ms.assetid: 579ef891-1f83-4c63-9ebd-2f40406b5b91
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 执行不区分区域性的字符串操作
默认情况下，执行区分区域性字符串操作的大多数 .NET Framework 方法都提供一些方法重载，通过传递一个 <xref:System.Globalization.CultureInfo> 参数，即可在这些方法重载中显式指定要使用的区域性。  这些重载允许您消除大小写映射和排序规则中的区域性差异，保证获得不区分区域性的结果。  
  
 本节提供了以下主题，用以说明如何使用默认区分区域性的 .NET Framework 方法执行不区分区域性的字符串操作。  
  
## 本节内容  
 [执行不区分区域性的字符串比较](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-comparisons.md)  
 描述如何使用 <xref:System.String.Compare%2A?displayProperty=fullName> 和 <xref:System.String.CompareTo%2A?displayProperty=fullName> 方法来执行不区分区域性的字符串比较。  
  
 [执行不区分区域性的大小写更改](../../../docs/standard/globalization-localization/performing-culture-insensitive-case-changes.md)  
 描述如何使用 <xref:System.String.ToUpper%2A?displayProperty=fullName>、<xref:System.String.ToLower%2A?displayProperty=fullName>、<xref:System.Char.ToUpper%2A?displayProperty=fullName> 和 <xref:System.Char.ToLower%2A?displayProperty=fullName> 方法来执行不区分区域性的大小写更改。  
  
 [在集合中执行不区分区域性的字符串操作](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-collections.md)  
 介绍如何使用 [CaseInsensitiveComparer 类](frlrfSystemCollectionsCaseInsensitiveComparerClassTopic)、<xref:System.Collections.CaseInsensitiveHashCodeProvider> 类、[SortedList 类](frlrfSystemCollectionsSortedListClassTopic)、[ArrayList.Sort 方法](https://msdn.microsoft.com/en-us/library/system.collections.arraylist.sort.aspx)和 [CollectionsUtil.CreateCaseInsensitiveHashtable 方法](frlrfSystemCollectionsSpecializedCollectionsUtilClassCreateCaseInsensitiveHashtableTopic)在集合中执行不区分区域性的操作。  
  
 [在数组中执行不区分区域性的字符串操作](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-arrays.md)  
 描述如何使用 <xref:System.Array.Sort%2A?displayProperty=fullName> 和 <xref:System.Array.BinarySearch%2A?displayProperty=fullName> 方法在数组中执行不区分区域性的操作。  
  
## 相关章节  
 [不区分区域性的字符串操作](../../../docs/standard/globalization-localization/culture-insensitive-string-operations.md)  
 介绍了对字符串执行操作时应了解区域性的原因，并为何时执行区分区域性的操作、何时执行不区分区域性的操作提供了指南。