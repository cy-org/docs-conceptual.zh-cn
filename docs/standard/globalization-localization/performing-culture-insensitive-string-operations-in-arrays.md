---
title: "在数组中执行不区分区域性的字符串操作 | Microsoft Docs"
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
  - "数组 [.NET Framework], 不区分区域性的字符串操作"
  - "比较器参数"
  - "不区分区域性的字符串操作, 在数组中"
ms.assetid: f12922e1-6234-4165-8896-63f0653ab478
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# 在数组中执行不区分区域性的字符串操作
默认情况下，<xref:System.Array.Sort%2A?displayProperty=fullName> 和 <xref:System.Array.BinarySearch%2A?displayProperty=fullName> 方法的重载使用 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=fullName> 属性执行区分区域性的排序。  由于排序顺序的不同，由这些方法返回的区分区域性的结果可能会因区域性而异。  若要消除区分区域性的行为，请使用此方法中接受 `comparer` 参数的重载之一。  `comparer` 参数指定比较数组中的元素时要使用的 <xref:System.Collections.IComparer> 实现。  对于该参数，请指定使用 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 的自定义固定比较器类。  [在集合中执行不区分区域性的字符串操作](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-collections.md)主题中的“使用 SortedList 类”子主题提供了自定义固定比较器类的示例。  
  
 **注意** 将 **CultureInfo.InvariantCulture** 传递给比较方法时，将执行不区分区域性的比较。  但是，这样做不会导致对文件路径、注册表项、环境变量等进行非语义比较，  也不支持基于比较结果的安全决策。  若要进行非语义比较或支持基于结果的安全决策，应用程序应使用接受 <xref:System.StringComparison> 值的比较方法。  因而，应用程序应传递 <xref:System.StringComparison>。  
  
## 请参阅  
 <xref:System.Array.Sort%2A?displayProperty=fullName>   
 <xref:System.Array.BinarySearch%2A?displayProperty=fullName>   
 <xref:System.Collections.IComparer>   
 [执行不区分区域性的字符串操作](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)