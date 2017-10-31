---
title: "&lt;TimeSpan_LegacyFormatMode&gt; 元素 | Microsoft Docs"
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
  - "<TimeSpan_LegacyFormatMode> 元素"
  - "TimeSpan_LegacyFormatMode 元素"
ms.assetid: 865e7207-d050-4442-b574-57ea29d5e2d6
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# &lt;TimeSpan_LegacyFormatMode&gt; 元素
确定运行时是否使用 <xref:System.TimeSpan?displayProperty=fullName> 值在格式化操作时保留旧式行为。  
  
## 语法  
  
```  
<TimeSpan_LegacyFormatMode    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否对 <xref:System.TimeSpan?displayProperty=fullName> 值使用旧格式设置行为。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|运行时不会恢复旧的格式设置行为。|  
|`true`|运行时恢复旧的格式设置行为。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含关于运行时初始化选项的信息。|  
  
## 备注  
 从 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]开始，<xref:System.TimeSpan?displayProperty=fullName> 结构实现了 <xref:System.IFormattable> 接口，并支持标准和自定义格式字符串的格式设置操作。  如果分析方法遇到不受支持的格式说明符或格式字符串，则会引发 <xref:System.FormatException>。  
  
 在以前版本的 .NET Framework 中，<xref:System.TimeSpan> 结构未实现 <xref:System.IFormattable>，且不支持格式字符串。  但是，许多开发人员错误地假定 <xref:System.TimeSpan> 确实支持格式字符串集以及通过 <xref:System.String.Format%2A?displayProperty=fullName> 等方法将其用于[复合格式操作](../../../../../docs/standard/base-types/composite-formatting.md)。  通常，如果一个类型实现 <xref:System.IFormattable> 并且支持格式字符串，使用不受支持的格式字符串调用格式设置方法通常将引发 <xref:System.FormatException>。  但是，由于 <xref:System.TimeSpan> 未实现 <xref:System.IFormattable>，所以运行时将忽略格式字符串，并改调 <xref:System.TimeSpan.ToString?displayProperty=fullName> 方法。  这意味着，虽然格式字符串对格式设置操作没左右，其存在不会导致 <xref:System.FormatException>。  
  
 对于旧式代码传递复合格式化方法和无效格式字符串的情况，且该代码未重新编译，则您可以使用 `<TimeSpan_LegacyFormatMode>` 元素恢复旧式 <xref:System.TimeSpan> 行为。  如果将该元素的 `enabled` 特性设置为 `true`，组合的格式化方法将导致对 <xref:System.TimeSpan.ToString?displayProperty=fullName> 的调用，而不是 <xref:System.TimeSpan.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName>，并且不会引发 <xref:System.FormatException>。  
  
## 示例  
 下面的示例实例化 <xref:System.TimeSpan> 对象，并尝试使用不受支持的标准格式字符串通过 <xref:System.String.Format%28System.String%2CSystem.Object%29?displayProperty=fullName> 方法来设置其格式。  
  
 [!code-csharp[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/timespan.breakingchanges/cs/legacyformatmode1.cs#1)]
 [!code-vb[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/timespan.breakingchanges/vb/legacyformatmode1.vb#1)]  
  
 如果在 [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)] 或较早版本上运行示例，则显示以下输出：  
  
```  
12:30:45  
```  
  
 如果在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]或以后版本上运行示例，则此与输出明显不同：  
  
```  
Invalid Format  
```  
  
 但是，如果将下面的配置文件添加到示例的目录中，并在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]或以后版本上运行该示例，则输出将与在 [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)] 上运行的示例时产生的相同。  
  
```  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <TimeSpan_LegacyFormatMode enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)