---
title: "&lt;gcServer&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/gcServer"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#gcServer"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<gcServer> 元素"
  - "gcServer 元素"
ms.assetid: 8d25b80e-2581-4803-bd87-a59528e3cb03
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# &lt;gcServer&gt; 元素
指定公共语言运行时是否运行服务器垃圾回收。  
  
## 语法  
  
```  
<gcServer    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否运行服务器垃圾回收。|  
  
## enabled 特性  
  
|值|描述|  
|-------|--------|  
|`false`|请勿运行服务器垃圾回收。  这是默认设置。|  
|`true`|运行服务器垃圾回收。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 公共语言运行时 \(CLR\) 支持两种类型的垃圾回收：工作站垃圾回收（适用于所有系统）和服务器垃圾回收（适用于多处理器系统）。  使用 `<gcServer>` 元素以控制 CLR 执行的垃圾回收类型。  使用 <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=fullName> 属性以确定是否启用服务器垃圾回收。  
  
 对于单处理器计算机，默认的工作站垃圾回收应该是最快捷的选项。  对于双处理器计算机，最快捷的选项既可以是工作站垃圾回收又可以是服务器垃圾回收。  对于两个以上处理器的计算机，服务器垃圾回收应该是最快捷的选项。  
  
 此元素只能在应用程序配置文件中使用；如果此元素在计算机配置文件中，请忽略。  
  
> [!NOTE]
>  在 .NET Framework 4 和更低版本中，启用服务器垃圾回收之后，并发垃圾回收不可用。  自 [!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)] 起，服务器垃圾回收就是并发回收。  若要使用非并发服务器垃圾回收，请将 `<gcServer>` 元素设置为  `true` 并将 [\<gcConcurrent\> 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md)设置为 `false`。  
  
## 示例  
 下面的示例启用服务器垃圾回收。  
  
```  
  
<configuration>  
   <runtime>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
  
```  
  
## 请参阅  
 <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=fullName>   
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [How to: Disable Concurrent Garbage Collection](http://msdn.microsoft.com/zh-cn/ba2c6c67-5778-497c-9fac-5f793b5500c7)