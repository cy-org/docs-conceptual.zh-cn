---
title: "&lt;shadowCopyVerifyByTimestamp&gt; 元素 | Microsoft Docs"
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
  - "<shadowCopyTimeStampVerification> 元素"
  - "shadowCopyTimeStampVerification 元素"
ms.assetid: 2f1648e5-997b-435e-a4f9-d236c574c66c
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;shadowCopyVerifyByTimestamp&gt; 元素
指定是否影像复制在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 中用引入的默认启动行为，或恢复为 .NET Framework 早期版本的启动行为。  
  
## 语法  
  
```  
<shadowCopyVerifyByTimestamp enabled="true|false" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|enabled|必需的特性。<br /><br /> 指定当启动时使用卷影复制比较程序集时间戳的应用程序域，以确定在卷影复制程序集之前是否已更新程序集。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|true|启动时，仅复制已更新的程序集，因为它们上次复制到了卷影复制目录。  这是 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 的默认值。|  
|false|恢复至之前 .NET Framework 版本的启动行为，其会在启动时复制所有文件。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 可以从 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 开始，影像复制程序集，仅当其时间戳表明它们自最后一次复制到卷影复制目录已更改时。  这将改善使用影像复制的众多应用程序的启动时间，如[影像复制程序集](../../../../../docs/framework/app-domains/shadow-copy-assemblies.md)中所述。  有高百分比和高频率的程序集更新的应用程序在行为中将不会从这个改变中收益。  那个实例中，可以使用这个元素存储.NET Framework的原来版本的行为。  
  
## 示例  
 下面的示例示出了如何禁用 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 中影像复制的默认启动行为，并恢复至之前 .NET Framework 版本的启动行为。  
  
```  
<configuration>  
   <runtime>  
      <shadowCopyVerifyByTimestamp enabled="false" />  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [影像复制程序集](../../../../../docs/framework/app-domains/shadow-copy-assemblies.md)