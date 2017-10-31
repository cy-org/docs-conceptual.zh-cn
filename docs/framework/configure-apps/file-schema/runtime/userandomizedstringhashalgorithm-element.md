---
title: "&lt;UseRandomizedStringHashAlgorithm&gt; 元素 | Microsoft Docs"
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
  - "<UseRandomizedStringHashAlgorithm> 元素"
  - "UseRandomizedStringHashAlgorithm 元素"
ms.assetid: c08125d6-56cc-4b23-b482-813ff85dc630
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# &lt;UseRandomizedStringHashAlgorithm&gt; 元素
确定公共语言运行时是否在每个应用程序域的基础上计算字符串的哈希代码。  
  
## 语法  
  
```  
<UseRandomizedStringHashAlgorithm   
   enabled=0|1 />  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定是否在每个应用程序域基础上计算字符串的哈希代码。|  
  
## enabled 特性  
  
|值|描述|  
|-------|--------|  
|`0`|公共语言运行时不根据每个应用程序域计算字符串的哈希代码；单个算法用于计算字符串哈希代码。  这是默认设置。|  
|`1`|公共语言运行时在每个应用程序域的基础上能够计算字符串的哈希代码。  不同应用程序域和不同进程中的相同字符串将具有不同的哈希代码。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含关于运行时初始化选项的信息。|  
  
## 备注  
 默认情况下，<xref:System.StringComparer> 类和 <xref:System.String.GetHashCode%2A?displayProperty=fullName> 方法使用可跨应用程序域生成一致的哈希代码的单个哈希算法。  这与将 `<UseRandomizedStringHashAlgorithm>` 元素的 `enabled` 特性设置为 `0` 是等效的。  这是 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 中所用的哈希算法。  
  
 <xref:System.StringComparer> 类和 <xref:System.String.GetHashCode%2A?displayProperty=fullName> 方法也可在每个应用程序域基础上使用计算哈希代码的不同哈希算法。  因此，不同的应用程序域中的等效字符串的哈希代码不同。  这是选择加入的功能；若要利用它，则必须将 `<UseRandomizedStringHashAlgorithm>` 元素的 `enabled` 特性设置为 `1`。  
  
 哈希表中的字符串查找通常为 O \(1\) 操作。  但是，当出现大量冲突时，查找会变为 O\(n<sup>2</sup>\) 操作。  您可以使用 `<UseRandomizedStringHashAlgorithm>` 配置元素根据应用程序域生成随机哈希算法，从而限制潜在冲突数，特别是在用于计算哈希代码的项基于用户输入数据的情况下。  
  
## 示例  
 下面的示例定义一个包含私有字符串常量 `s` 的 `DisplayString` 类，其值为“这是字符串”。它还包括显示字符串值及其哈希代码的 `ShowStringHashCode` 方法以及该方法在其中执行的应用程序域的名称。  
  
 [!code-csharp[System.String.GetHashCode#2](../../../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.String.GetHashCode/CS/perdomain.cs#2)]
 [!code-vb[System.String.GetHashCode#2](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.String.GetHashCode/VB/perdomain.vb#2)]  
  
 当您在未提供配置文件的情况下运行该示例时，它会显示类似下面的输出。  请注意，字符串的散列码在两个应用程序域中是相同的。  
  
```  
  
String 'This is a string.' in domain 'PerDomain.exe': 941BCEAC  
String 'This is a string.' in domain 'NewDomain': 941BCEAC  
  
```  
  
 但是，如果将以下配置文件添加到示例目录，然后运行该示例，则同一个字符串的哈希代码将通过应用程序域进行区分。  
  
```  
  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <UseRandomizedStringHashAlgorithm enabled="1" />  
   </runtime>  
</configuration>  
  
```  
  
 存在配置文件时，示例会显示以下输出：  
  
```  
  
String 'This is a string.' in domain 'PerDomain.exe': 5435776D  
String 'This is a string.' in domain 'NewDomain': 75CC8236  
  
```  
  
## 请参阅  
 <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName>   
 <xref:System.String.GetHashCode%2A?displayProperty=fullName>   
 <xref:System.Object.GetHashCode%2A?displayProperty=fullName>