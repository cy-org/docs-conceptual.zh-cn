---
title: "&lt;disableFusionUpdatesFromADManager&gt; 元素 | Microsoft Docs"
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
  - "<disableFusionUpdatesFromADManager> 元素"
  - "disableFusionUpdatesFromADManager 元素"
ms.assetid: 58d2866c-37bd-4ffa-abaf-ff35926a2939
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;disableFusionUpdatesFromADManager&gt; 元素
指定是否禁用默认行为，此行为允许运行时主机重写应用程序域的配置设置。  
  
## 语法  
  
```  
<disableFusionUpdatesFromADManager enabled="0|1"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|enabled|必需的特性。<br /><br /> 指定是否禁用用于重写合成设置的默认功能。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|0|不禁用用于重写合成设置的功能。  从 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]开始，这是默认行为。|  
|1|禁用用于重写合成设置的功能。  这将恢复为早期版本的 .NET Framework 的行为。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 从 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]开始，默认行为是允许 <xref:System.AppDomainManager> 对象通过以下方式重写配置设置：在 <xref:System.AppDomainManager> 的子类中，使用传递给 <xref:System.AppDomainManager.InitializeNewDomain%2A?displayProperty=fullName> 方法的实现的 <xref:System.AppDomainSetup> 对象的 <xref:System.AppDomainSetup.ConfigurationFile%2A> 属性或 <xref:System.AppDomainSetup.SetConfigurationBytes%2A> 方法。  对于默认应用程序域，您更改的设置会重写由应用程序配置文件指定的设置。  对于其他应用程序域，您更改的设置会重写已传递给 <xref:System.AppDomainManager.CreateDomain%2A?displayProperty=fullName> 或 <xref:System.AppDomain.CreateDomain%2A?displayProperty=fullName> 方法的配置设置。  
  
 您可以传递新的配置信息或传递 null（在 Visual Basic 中为 `Nothing`）来消除已传入的配置信息。  
  
 不要将配置信息传递给 <xref:System.AppDomainSetup.ConfigurationFile%2A> 属性和 <xref:System.AppDomainSetup.SetConfigurationBytes%2A> 方法。  如果将配置信息传递给这二者，则会忽略传递给 <xref:System.AppDomainSetup.ConfigurationFile%2A> 属性的信息，这是因为 <xref:System.AppDomainSetup.SetConfigurationBytes%2A> 方法会重写应用程序配置文件中的配置信息。  如果使用 <xref:System.AppDomainSetup.ConfigurationFile%2A> 属性，则可以将 null（在 Visual Basic 中为 `Nothing`）传递给 <xref:System.AppDomainSetup.SetConfigurationBytes%2A> 方法，从而消除在对 <xref:System.AppDomainManager.CreateDomain%2A?displayProperty=fullName> 或 <xref:System.AppDomain.CreateDomain%2A?displayProperty=fullName> 方法的调用中已指定的任何配置字节。  
  
 除了配置信息之外，您还可以更改传递给 <xref:System.AppDomainManager.InitializeNewDomain%2A?displayProperty=fullName> 方法的实现的 <xref:System.AppDomainSetup> 对象上的以下设置：<xref:System.AppDomainSetup.ApplicationBase%2A>、<xref:System.AppDomainSetup.ApplicationName%2A>、<xref:System.AppDomainSetup.CachePath%2A>、<xref:System.AppDomainSetup.DisallowApplicationBaseProbing%2A>、<xref:System.AppDomainSetup.DisallowBindingRedirects%2A>、<xref:System.AppDomainSetup.DisallowCodeDownload%2A>、<xref:System.AppDomainSetup.DisallowPublisherPolicy%2A>、<xref:System.AppDomainSetup.DynamicBase%2A>、<xref:System.AppDomainSetup.LoaderOptimization%2A>、<xref:System.AppDomainSetup.PrivateBinPath%2A>、<xref:System.AppDomainSetup.PrivateBinPathProbe%2A>、<xref:System.AppDomainSetup.ShadowCopyDirectories%2A> 和 <xref:System.AppDomainSetup.ShadowCopyFiles%2A>。  
  
 作为使用 `<disableFusionUpdatesFromADManager>` 元素的替代方法，您可以通过创建注册表设置或通过设置环境变量来禁用默认行为。  在注册表中，在 `HKCU\Software\Microsoft\.NETFramework` 或 `HKLM\Software\Microsoft\.NETFramework` 下创建一个名为 `COMPLUS_disableFusionUpdatesFromADManager` 的 DWORD 值，并将此值设置为 1。  在命令行上，将环境变量 `COMPLUS_disableFusionUpdatesFromADManager` 设置为 1。  
  
## 示例  
 下面的代码示例演示如何通过使用 `<disableFusionUpdatesFromADManager>` 元素来禁用用于重写合成设置的功能。  
  
```  
<configuration>  
   <runtime>  
      <disableFusionUpdatesFromADManager enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [运行时如何定位程序集](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)