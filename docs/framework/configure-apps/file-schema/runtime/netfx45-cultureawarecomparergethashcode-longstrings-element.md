---
title: "&lt;NetFx45_CultureAwareComparerGetHashCode_LongStrings&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "NetFx45_CultureAwareComparerGetHashCode_LongStrings 元素"
  - "<NetFx45_CultureAwareComparerGetHashCode_LongStrings> 元素"
  - "GetHashCode 方法"
  - "哈希代码, 计算"
ms.assetid: 3a5f38d1-ebc8-44de-aaeb-2929f6e6b48f
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# &lt;NetFx45_CultureAwareComparerGetHashCode_LongStrings&gt; 元素
指定运行时是否使用固定的内存量来计算 <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName> 方法的哈希代码。  
  
 \<configuration\>  
\<runtime\>  
\<NetFx45\_CultureAwareComparerGetHashCode\_LongStrings\>  
  
## 语法  
  
```vb  
<NetFx45_CultureAwareComparerGetHashCode_LongStrings enabled="0|1">  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定公共语言运行时是否在计算哈希代码时分配固定的内存量。|  
  
## enabled 特性  
  
|值|描述|  
|-------|--------|  
|0|公共语言运行时为 <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName> 方法分配可变的内存量来计算哈希代码。 这是默认设置。|  
|1|公共语言运行时为 <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName> 方法分配固定的内存量来计算哈希代码。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
  
## 备注  
 默认情况下，公共语言运行时将为 <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName> 方法分配可变的内存量，当该方法尝试计算非常大的字符串（几百万个字符以上）的哈希代码时，会引发 <xref:System.ArgumentException>。 通过将此元素添加到应用程序配置文件并将其 `enabled` 特性设置为“1”，你可以指定 <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName> 方法使用可分配固定内存量以计算哈希代码的替代算法。  
  
> [!IMPORTANT]
>  `<NetFx45_CultureAwareComparerGetHashCode_LongStrings>` 元素不在 [!INCLUDE[win8](../../../../../includes/win8-md.md)] 和更高版本中使用。  
  
## 请参阅  
 <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName>   
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)