---
title: "&lt;alwaysFlowImpersonationPolicy&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/alwaysFlowImpersonationPolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#alwaysFlowImpersonationPolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<alwaysFlowImpersonationPolicy> 元素"
  - "alwaysFlowImpersonationPolicy 元素"
ms.assetid: ee622801-9e46-470b-85ab-88c4b1dd2ee1
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;alwaysFlowImpersonationPolicy&gt; 元素
指定无论模拟是如何执行的，Windows 标识始终流经异步点。  
  
## 语法  
  
```  
<alwaysFlowImpersonationPolicy    
  enabled="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指示 Windows 标识是否流经异步点。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|Windows 标识不流经异步点，除非模拟是通过诸如 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A> 这样的托管方法执行的。  这是默认值。|  
|`true`|无论模拟是如何执行的，Windows 标识始终流经异步点。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 在 .NET Framework 1.0 和 1.1 版中，Windows 标识不流经异步点。  在 .NET Framework 2.0 版中，有一个包含关于当前执行线程的信息的 <xref:System.Threading.ExecutionContext> 对象，并且它流经应用程序域中的异步点。  只要模拟是使用托管方法（如 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A>）而不是通过其他途径（如对本机方法的平台调用）实现的，则 <xref:System.Security.Principal.WindowsIdentity> 还将作为流经异步点的信息的一部分流动。  此元素用于指定无论模拟是如何实现的，Windows 标识总要流经异步点。  
  
 还可以通过两种方式改变这种默认行为：  
  
1.  在托管代码中在每个线程的基础上改变。  
  
     通过使用 <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=fullName>、<xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=fullName> 或 <xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=fullName> 方法修改 <xref:System.Threading.ExecutionContext> 和 <xref:System.Security.SecurityContext> 设置，可以在每个线程的基础上取消流。  
  
2.  在调用非托管承载接口，以加载公共语言运行时 \(CLR\) 时改变。  
  
     如果使用非托管承载接口而非简单的托管可执行文件来加载 CLR，可以在对 [CorBindToRuntimeEx 函数](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) 函数的调用中指定一个特殊标记。  若要对整个过程启用兼容模式，应将 [CorBindToRuntimeEx 函数](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) 的 `flags` 参数设置为 STARTUP\_ALWAYSFLOW\_IMPERSONATION。  
  
## 配置文件  
 此元素只可用于应用程序配置文件中。  
  
## 示例  
 下面的示例演示如何指定 Windows 标识流经异步点 \-\- 即使模拟是通过除托管方法以外的途径实现的也如此。  
  
```  
<configuration>  
  <runtime>  
    <alwaysFlowImpersonationPolicy enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<legacyImpersonationPolicy\> 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/legacyimpersonationpolicy-element.md)