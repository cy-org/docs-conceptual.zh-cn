---
title: "执行不区分区域性的大小写更改 | Microsoft Docs"
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
  - "String.ToLower 方法"
  - "区域性，区分大小写"
  - "Char.ToLower 方法"
  - "大小写，在不区分区域性的字符串中更改"
  - "Char.ToUpper 方法"
  - "不区分区域性的字符串操作，大小写更改"
  - "String.ToUpper 方法"
  - "区域性参数"
ms.assetid: 822d551c-c69a-4191-82f4-183d82c9179c
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# 执行不区分区域性的大小写更改
<xref:System.String.ToUpper%2A?displayProperty=fullName>、<xref:System.String.ToLower%2A?displayProperty=fullName>、<xref:System.Char.ToUpper%2A?displayProperty=fullName> 和 <xref:System.Char.ToLower%2A?displayProperty=fullName> 方法提供不接受任何参数的重载。  默认情况下，这些没有参数的重载会根据 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 的值来执行大小写更改。  这样，会生成因区域性而异的区分大小写的结果。  若要明确指出您是希望大小写更改区分区域性还是希望它不区分区域性，您应该使用这些方法的重载，这些重载要求您显式指定 `culture` 参数。  对于区分区域性的大小写更改，请为 `culture` 参数指定 `CultureInfo.CurrentCulture`。  对于不区分区域性的大小写更改，请为 `culture` 参数指定 `CultureInfo.InvariantCulture`。  
  
 通常，会将字符串转换成标准大小写，以便更易于以后查找。  以这种方式使用字符串时，应该为 `culture` 参数指定 `CultureInfo.InvariantCulture`，这是因为从更改大小写到进行查找的这段时间内，<xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=fullName> 的值可能更改。  
  
 如果安全决策基于大小写更改操作，则该操作不应区分区域性，以确保结果不受 `CultureInfo.CurrentCulture` 值的影响。  有关说明不区分区域性的字符串操作如何产生不一致结果的示例，请参见[针对使用字符串的最佳做法](../../../docs/standard/base-types/best-practices-strings.md)文章的“使用当前区域性的字符串比较”部分。  
  
## 使用 String.ToUpper 和 String.ToLower 方法  
 为了使代码清楚，建议您始终使用 `String.ToUpper` 和 `String.ToLower` 方法的重载，这些重载允许您显式指定 `culture` 参数。  例如，下面的代码执行了标识符查找操作。  `key.ToLower` 操作在默认情况下是区分区域性的，但是对于读取代码，此行为并非很有把握。  
  
### 示例  
  
```vb  
Shared Function LookupKey(key As String) As Object  
   Return internalHashtable(key.ToLower())  
End Function  
  
```  
  
```csharp  
static object LookupKey(string key)   
{  
    return internalHashtable[key.ToLower()];  
}  
```  
  
 如果您希望 `key.ToLower` 操作不区分区域性，应该如下所述更改前面的示例，以便在更改大小写时显式使用 `CultureInfo.InvariantCulture`。  
  
```vb  
Shared Function LookupKey(key As String) As Object  
    Return internalHashtable(key.ToLower(CultureInfo.InvariantCulture))  
End Function  
  
```  
  
```csharp  
static object LookupKey(string key)   
{  
    return internalHashtable[key.ToLower(CultureInfo.InvariantCulture)];  
}  
```  
  
## 使用 Char.ToUpper 和 Char.ToLower 方法  
 尽管 `Char.ToUpper` 和 `Char.ToLower` 方法与 `String.ToUpper` 和 `String.ToLower` 方法具有相同的特性，但受影响的区域性只有土尔其语（土尔其）和阿塞拜疆（拉丁，阿塞拜疆）。  这是仅有的两个具有单个字符大小写区别的区域性。  有关这个唯一大小写映射的详细信息，请参见 <xref:System.String> 中的“自定义大小写映射和排序规则”。  为使代码清晰并确保结果一致，建议始终使用这些方法的重载，以便显式指定 `culture` 参数。  
  
## 请参阅  
 <xref:System.String.ToUpper%2A?displayProperty=fullName>   
 <xref:System.String.ToLower%2A?displayProperty=fullName>   
 <xref:System.Char.ToUpper%2A?displayProperty=fullName>   
 <xref:System.Char.ToLower%2A?displayProperty=fullName>   
 [执行不区分区域性的字符串操作](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)