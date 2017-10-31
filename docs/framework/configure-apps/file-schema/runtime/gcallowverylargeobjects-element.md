---
title: "&lt;gcAllowVeryLargeObjects&gt; 元素 | Microsoft Docs"
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
  - "<gcAllowVeryLargeObjects> 元素"
  - "gcAllowVeryLargeObjects 元素"
ms.assetid: 5c7ea24a-39ac-4e5f-83b7-b9f9a1b556ab
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# &lt;gcAllowVeryLargeObjects&gt; 元素
在64位平台上，可以允许总共大于2千兆字节的数组。  
  
## 语法  
  
```  
<gcAllowVeryLargeObjects    
   enabled="true|false" />  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定总大小大于 2 GB的数组是否可以在 64 位平台上。|  
  
## enabled 特性  
  
|值|描述|  
|-------|--------|  
|`false`|总大小超过2GB的数组是不被允许的。  这是默认值。|  
|`true`|总大小大于2GB的数组在64位平台上是被允许的。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含关于运行时初始化选项的信息。|  
  
## 备注  
 通过在应用程序的配置文件使用此元素启用超过 2 GB 的大小的数组，但是这不会更改对象范围或数组大小的其他限制：  
  
-   数组中的元素最大值是 <xref:System.UInt32.MaxValue?displayProperty=fullName>。  
  
-   在所有一维的字节数组和数组的单字节结构最大索引为 2,147,483,591 \(0x7FFFFFC7\)， 其他类型的索引为2,146,435,071 \(0X7FEFFFFF\)。  
  
-   字符串和其他非数组对象的最大大小保持不变。  
  
> [!CAUTION]
>  在启用此功能之前，请确保您的应用程序不包括不安全代码，假定所有数组的大小小于 2 GB。  例如，使用不安全的数组代码作为缓冲区，可能容易引起缓冲区溢出，假设编写数组不会超过 2 GB。  
  
## 示例  
 下面的示例演示如何为某个应用程序启用这项功能。  
  
```  
<configuration>  
  <runtime>  
    <gcAllowVeryLargeObjects enabled="true" />  
  </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)