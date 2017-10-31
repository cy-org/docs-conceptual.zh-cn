---
title: "&lt;disableCommitThreadStack&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCommitThreadStack"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCommitThreadStack"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<disableCommitThreadStack> 元素"
  - "disableCommitThreadStack 元素"
ms.assetid: 3559d46a-7640-4c72-9a11-7e980768929e
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# &lt;disableCommitThreadStack&gt; 元素
指定在线程启动时是否提交完整线程堆栈。  
  
 \<configuration\>  
\<runtime\>  
\<disableCommitThreadStack\>  
  
## 语法  
  
```  
<disableCommitThreadStack enabled="0|1"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|enabled|必需的特性。<br /><br /> 指定是否禁止在线程启动时提交完整线程堆栈（默认行为）。|  
  
## enabled 特性  
  
|值|描述|  
|-------|--------|  
|0|不禁用公共语言运行时的默认行为（即在线程启动时提交完整线程堆栈）。|  
|1|禁用公共语言运行时的默认行为（即在线程启动时提交完整线程堆栈）。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 公共语言运行时的默认行为是在线程启动时提交完整线程堆栈。 当必须在内存有限的服务器上创建大量线程，并且其中大多数线程都使用非常小的堆栈空间时，如果公共语言运行时在线程启动时不立即提交完整线程堆栈，则服务器可能会表现更好。  
  
> [!NOTE]
>  非托管主机可以使用 [STARTUP\_FLAGS](../../../../../ocs/framework/unmanaged-api/hosting/startup-flags-enumeration.md) 枚举中的 `STARTUP_DISABLE_COMMITTHREADSTACK` 启动标志实现相同结果。  
  
## 示例  
 下面的示例演示如何禁用公共语言运行时的默认行为（即在线程启动时提交完整线程堆栈）。  
  
```  
<configuration>  
   <runtime>  
      <disableCommitThreadStack enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)