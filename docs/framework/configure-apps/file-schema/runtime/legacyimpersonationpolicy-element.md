---
title: "&lt;legacyImpersonationPolicy&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#legacyImpersonationPolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/legacyImpersonationPolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<legacyImpersonationPolicy> 元素"
  - "legacyImpersonationPolicy 元素"
ms.assetid: 6e00af10-42f3-4235-8415-1bb2db78394e
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# &lt;legacyImpersonationPolicy&gt; 元素
指定无论当前线程上的执行上下文的流设置如何，Windows 标识都不流经异步点。  
  
## 语法  
  
```  
<legacyImpersonationPolicy    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定无论当前线程上的 <xref:System.Threading.ExecutionContext> 流设置如何，<xref:System.Security.Principal.WindowsIdentity> 都不流经异步点。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|<xref:System.Security.Principal.WindowsIdentity> 根据当前线程的 <xref:System.Threading.ExecutionContext> 流设置确定是否流经异步点。  这是默认值。|  
|`true`|<xref:System.Security.Principal.WindowsIdentity> 无论当前线程上的 <xref:System.Threading.ExecutionContext> 流设置如何都不流经异步点。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 在 .NET Framework 1.0 和 1.1 版中，<xref:System.Security.Principal.WindowsIdentity> 不流经任何用户定义的异步点。  在 .NET Framework 2.0 版中，有一个包含关于当前执行线程的信息的 <xref:System.Threading.ExecutionContext> 对象，并且它流经应用程序域中的异步点。  <xref:System.Security.Principal.WindowsIdentity> 也作为流经异步点的信息的一部分流动，这意味着如果模拟上下文退出，它仍会流动。  此元素用于指定 <xref:System.Security.Principal.WindowsIdentity> 不流经异步点。  
  
> [!NOTE]
>  此公共语言运行时 \(CLR\) 会察觉仅使用托管代码执行的模拟操作，不会察觉在托管代码以外执行的模拟，如通过平台调用非托管代码或通过直接调用 Win32 函数。  只有托管 <xref:System.Security.Principal.WindowsIdentity> 对象可以流经异步点，除非 `alwaysFlowImpersonationPolicy` 元素已设置为 true \(`<alwaysFlowImpersonationPolicy enabled="true"/>`\)。  将 `alwaysFlowImpersonationPolicy` 元素设置为 true 会指定无论模拟是如何执行的，Windows 标识始终流经异步点。  有关使非托管模拟流经异步点的更多信息，请参见 [\<alwaysFlowImpersonationPolicy\> 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/alwaysflowimpersonationpolicy-element.md)。  
  
 此元素只可用于应用程序配置文件中。  
  
 还可以通过两种方式改变这种默认行为：  
  
1.  在托管代码中在每个线程的基础上改变。  
  
     通过使用 <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=fullName>、<xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=fullName> 或 <xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=fullName> 方法修改 <xref:System.Threading.ExecutionContext> 和 <xref:System.Security.SecurityContext> 设置，可以在每个线程的基础上取消流。  
  
2.  在调用非托管承载接口，以加载公共语言运行时 \(CLR\) 时改变。  
  
     如果使用非托管承载接口而非简单的托管可执行文件来加载 CLR，可以在对 [CorBindToRuntimeEx 函数](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) 函数的调用中指定一个特殊标记。  若要对整个过程启用兼容模式，应将 [CorBindToRuntimeEx 函数](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) 的 `flags` 参数设置为 STARTUP\_LEGACY\_IMPERSONATION。  
  
## 示例  
 下面的示例演示如何指定不让 Windows 标识流经异步点的旧式行为。  
  
```  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)