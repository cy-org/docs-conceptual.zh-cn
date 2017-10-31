---
title: "&lt;supportedRuntime&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#supportedRuntime"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/supportedRuntime"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<supportedRuntime> 元素"
  - "supportedRuntime 元素"
ms.assetid: 1ae16e23-afbe-4de4-b413-bc457f37b69f
caps.latest.revision: 33
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 28
---
# &lt;supportedRuntime&gt; 元素
指定应用程序支持的公共语言运行时版本。 此元素应由用 .NET Framework 1.1 版或更高版本生成的所有应用程序使用。  
  
 [\<configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<startup\>](../../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)  
  
 **\<supportedRuntime\>**  
  
## 语法  
  
```  
  
<supportedRuntime version="runtime version" sku="sku id"/>  
```  
  
## 特性  
  
|特性|描述|  
|--------|--------|  
|**version**|可选特性。<br /><br /> 一个字符串值，它指定此应用程序支持的公共语言运行时 \(CLR\) 版本。 有关 `version` 特性的有效值的信息，请参阅[“运行时版本”值](#version)部分。 **Note:**  通过 .NET Framework 3.5，“*运行时版本*”值的形式为*主版本号*.*次版本号*.*内部版本号*。 从 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 开始，仅主版本号和次版本号是必需的（即“v4.0”而不是“v4.0.30319”）。 建议使用较短字符串。|  
|**sku**|可选特性。<br /><br /> 一个字符串值，该值指定库存单位 \(SKU\)，库存单位则指定此应用程序支持的 .NET Framework 版本。<br /><br /> 从 .NET Framework 4.0 起，建议使用 `sku` 特性。  若存在该特性，则它指示应用面向的 .NET Framework 版本。<br /><br /> 有关 SKU 特性的有效值的信息，请参阅 [“SKU ID”值](#sku) 部分。|  
  
## 备注  
 如果应用程序配置文件中没有 **\<supportedRuntime\>** 元素，则使用用于生成应用程序的运行时版本。  
  
 **\< supportedRuntime\>** 元素应由使用运行时 1.1 版或更高版本生成的所有应用程序使用。 仅为支持运行时 1.0 版而生成的应用程序必须使用 [\<requiredRuntime\>](../../../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md) 元素。  
  
> [!NOTE]
>  如果使用 [CorBindToRuntimeByCfg](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md) 函数来指定配置文件，则必须使用适用于所有运行时版本的 `<requiredRuntime>` 元素。 当你使用 [CorBindToRuntimeByCfg](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md) 时，`<supportedRuntime>` 元素将被忽略。  
  
 对于支持从 .NET Framework 1.1 到 3.5 的运行时版本的应用，支持多个运行时版本时，第一个元素应指定优先级最高的版本，最后一个元素应指定优先级最低的版本。 对于支持 .NET Framework 4.0 或更高版本的应用，`version` 特性指示普遍适用于 .NET Framework 4 及更高版本的 CLR 版本，而 `sku` 特性指示应用所面向的单个 .NET Framework 版本。  
  
> [!NOTE]
>  如果你的应用程序使用旧式激活路径（如 [CorBindToRuntimeEx 函数](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)），并且你希望这些路径激活 CLR 的版本 4（而不是较早的版本），或者你的应用程序是用 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 生成的，但在使用较早版本的 .NET Framework 生成的混合模式程序集上有依赖项，则不足以在受支持的运行时列表中指定 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]。 此外，在配置文件的 [\<startup\> 元素](../../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)中，必须将 `useLegacyV2RuntimeActivationPolicy` 特性设置为 `true`。 但是，将此特性设置为 `true` 意味着，用 .NET Framework 早期版本生成的所有组件都使用 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]（而不是生成它们时所用的运行时）运行。  
  
 我们建议你使用应用程序可在其上运行的所有 .NET Framework 版本来测试这些应用程序。  
  
<a name="version"></a>   
## “运行时版本”值  
 下表列出了`version`特性的*运行时版本*值的有效值。  
  
|.NET Framework 版本|`version` 特性|  
|-----------------------|------------------|  
|1.0|"v1.0.3705"|  
|1.1|"v1.1.4322"|  
|2.0|"v2.0.50727"|  
|3.0|"v2.0.50727"|  
|3.5|"v2.0.50727"|  
|4.0|"v4.0"|  
|4.5|"v4.0"|  
|4.5.1|"v4.0"|  
|4.5.2|"v4.0"|  
|4.6|"v4.0"|  
|4.6.1|"v4.0"|  
  
<a name="sku"></a>   
## “SKU ID”值  
 下表列出 `sku` 特性支持的 .NET Framework 版本（自 .NET Framework 4 起）。  请注意，自 .NET Framework 4 开始的 `sku` 特性指示应用面向的 .NET Framework 版本。  
  
|.NET Framework 版本|`sku` 特性|  
|-----------------------|--------------|  
|4.0|".NETFramework,Version\=v4.0"|  
|4.0，客户端配置文件|".NETFramework,Version\=v4.0,Profile\=Client"|  
|4.0，平台更新 1|.NETFramework,Version\=v4.0.1|  
|4.0，客户端配置文件，Update 1|.NETFramework,Version\=v4.0.1,Profile\=Client|  
|4.0，平台更新 2|.NETFramework,Version\=v4.0.2|  
|4.0，客户端配置文件，Update 2|.NETFramework,Version\=v4.0.2,Profile\=Client|  
|4.0，平台更新 3|.NETFramework,Version\=v4.0.3|  
|4.0，客户端配置文件，Update 3|.NETFramework,Version\=v4.0.3,Profile\=Client|  
|4.5|".NETFramework,Version\=v4.5"|  
|4.5.1|".NETFramework,Version\=v4.5"|  
|4.5.2|".NETFramework,Version\=v4.5"|  
|4.6|".NETFramework,Version\=v4.5"|  
|4.6.1|".NETFramework,Version\=v4.5"|  
  
 下表显示对于不同的 `sku` 特性值，当 `version` 特性为 v4.0 且 `sku` 特性标识 .NET Framework 4 或它的一个平台更新 \(PU\) 时，应用程序将在安装的哪一个 .NET Framework 4 版本上运行。  
  
|`sku` 特性的值|4.0 Client|4.0 Full|4.0 Client \+ PU 1|4.0 Full \+ PU 1|4.0 Client \+ PU 2|4.0 Full \+ PU 2|4.0 Client \+ PU 3|4.0 Full \+ PU 3|4.5 和更高版本|  
|----------------|----------------|--------------|------------------------|----------------------|------------------------|----------------------|------------------------|----------------------|---------------|  
|.NETFramework,Version\=v4.0,Profile\=Client|是|是|是|是|是|是|是|是|是|  
|.NETFramework,Version\=v4.0||是||是||是||是|是|  
|.NETFramework,Version\=v4.0.1,Profile\=Client|||是|是|是|是|是|是|是|  
|.NETFramework,Version\=v4.0.1||||是||是||是|是|  
|.NETFramework,Version\=v4.0.2,Profile\=Client|||||是|是|是|是|是|  
|.NETFramework,Version\=v4.0.2||||||是||是|是|  
|.NETFramework,Version\=v4.0.3,Profile\=Client|||||||是|是|是|  
|.NETFramework,Version\=v4.0.3||||||||是|是|  
  
## 示例  
 下面的示例演示如何在配置文件中指定支持的运行时版本。 配置文件指示应用面向 .NET Framework 4.6。  
  
```xml  
  
<configuration> <startup> <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" /> </startup> </configuration>  
  
```  
  
## 配置文件  
 此元素可用于应用程序配置文件中。  
  
## 请参阅  
 [启动设置架构](../../../../../docs/framework/configure-apps/file-schema/startup/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<PaveOver\> 指定要使用的运行时版本](http://msdn.microsoft.com/zh-cn/c376208d-980d-42b4-865b-fbe0d9cc97c2)   
 [进程内并行执行](../../../../../docs/framework/deployment/in-process-side-by-side-execution.md)