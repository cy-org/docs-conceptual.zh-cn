---
title: "&lt;startup&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#startup"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<startup> 元素"
  - "容器标记, <startup> 元素"
  - "startup 元素"
ms.assetid: 536acfd8-f827-452f-838a-e14fa3b87621
caps.latest.revision: 19
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 19
---
# &lt;startup&gt; 元素
指定公共语言运行时启动信息。  
  
## 语法  
  
```  
<startup useLegacyV2RuntimeActivationPolicy="true|false" >   
</startup>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`useLegacyV2RuntimeActivationPolicy`|可选特性。<br /><br /> 指定是否启用 [!INCLUDE[dnprdnext](../../../../../includes/dnprdnext-md.md)] 运行时激活策略，或者是否使用 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 激活策略。|  
  
## useLegacyV2RuntimeActivationPolicy 特性  
  
|值|说明|  
|-------|--------|  
|`true`|为所选运行时启用 [!INCLUDE[dnprdnext](../../../../../includes/dnprdnext-md.md)] 运行时激活策略，该策略要将运行时激活技术（如 [CorBindToRuntimeEx 功能](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)）绑定到从配置文件选择的运行时，而不是将它们盖在 CLR 版本 2.0 上。  因此，如果从配置文件选择 CLR 版本 4 或更高版本，则使用 .NET Framework 的早期版本创建的混合模式程序集将与所选 CLR 版本一同加载。  设置此值可防止 CLR 版本 1.1 或 2.0 加载到同一进程，有效地禁用进程中的并行功能。|  
|`false`|使用 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 及更高版本的默认激活策略，即允许旧式运行时激活技术将 CLR 版本 1.1 或 2.0 加载到进程。  设置这个值阻止混合模式程序集加载到.NET Framework 4或以后的版本，除非他们以.NET Framework 4或以后的版本生成。  这值是默认值。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<requiredRuntime\>](../../../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md)|指定应用程序仅支持公共语言运行时 1.0 版。  以版本1.1或以后版本的运行时生成的应用程序应该使用**\<supportedRuntime\>**元素。|  
|[\<运行时\>](../../../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)|指定此应用程序支持的公共语言运行时版本。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
  
## 备注  
 **\< supportedRuntime\>**元素应由使用运行时 1.1 版或更高版本生成的所有应用程序使用。  仅为支持运行 1.0 版时而生成的应用程序必须使用 **\<requiredRuntime\>** 元素。  
  
 Microsoft Internet Explorer中的应用程序的开始代码忽略**\<startup\>**元素和它的子元素。  
  
## useLegacyV2RuntimeActivationPolicy 特性  
 如果您的应用程序使用旧式激活路径，如 [CorBindToRuntimeEx function（CorBindToRuntimeEx 功能）](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)，并且您希望这些路径激活 CLR 的版本 4（而不是较早的版本），或者如果您的应用程序是用 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 生成的，但在使用较早版本的 .NET Framework 生成的混合模式程序集上有依赖项，则此特性将派上用场。  在这些方案中，将特性设置为 `true`。  
  
> [!NOTE]
>  将该属性设置为 `true` 可以防止把 CLR 版本 1.1 或 CLR 版本 2.0 加载到同一进程，有效地禁用进程中的并行功能（请参见 [Side\-by\-Side Execution for COM Interop](http://msdn.microsoft.com/zh-cn/4302318c-3586-49bf-8620-b9a39cdf4a32)）。  
  
## 示例  
 下面的示例说明如何在配置文件中指定运行时版本。  
  
```  
<!-- When used with version 1.0 of the .NET Framework runtime -->  
<configuration>  
   <startup>  
      <requiredRuntime version="v1.0.3705" safemode="true"/>  
   </startup>  
</configuration>  
<!-- When used with version 1.1 (or later) of the runtime -->  
<configuration>  
   <startup>  
      <supportedRuntime version="v1.1.4322"/>  
      <supportedRuntime version="v1.0.3705"/>  
   </startup>  
</configuration>  
```  
  
## 请参阅  
 [启动设置架构](../../../../../docs/framework/configure-apps/file-schema/startup/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<PaveOver\> Specifying Which Runtime Version to Use](http://msdn.microsoft.com/zh-cn/c376208d-980d-42b4-865b-fbe0d9cc97c2)   
 [Side\-by\-Side Execution for COM Interop](http://msdn.microsoft.com/zh-cn/4302318c-3586-49bf-8620-b9a39cdf4a32)   
 [进程内并行执行](../../../../../docs/framework/deployment/in-process-side-by-side-execution.md)