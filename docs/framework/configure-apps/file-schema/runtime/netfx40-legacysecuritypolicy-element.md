---
title: "&lt;NetFx40_LegacySecurityPolicy&gt; 元素 | Microsoft Docs"
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
  - "<NetFx40_LegacySecurityPolicy> 元素"
  - "NetFx40_LegacySecurityPolicy 元素"
ms.assetid: 07132b9c-4a72-4710-99d7-e702405e02d4
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# &lt;NetFx40_LegacySecurityPolicy&gt; 元素
指定运行时是否使用旧版代码访问安全性 \(CAS\) 策略。  
  
## 语法  
  
```  
<NetFx40_LegacySecurityPolicy  
   enabled="true|false"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否使用旧版 CAS 策略。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|运行时不使用旧版 CAS 策略。  这是默认设置。|  
|`true`|运行时使用旧版 CAS 策略。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含关于运行时初始化选项的信息。|  
  
## 备注  
 在 .NET Framework 版本 3.5 和早期版本中，CAS 策略始终有效。  在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]中，必须启用 CAS 策略。  
  
 CAS 策略将因版本而异。  在 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 中，必须重新指定存在于早期版本的 .NET Framework 中的自定义 CAS 策略。  
  
 将 `<NetFx40_LegacySecurityPolicy>` 元素应用于 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 程序集不会影响 [安全透明代码](../../../../../docs/framework/misc/security-transparent-code.md)；透明度规则仍然适用。  
  
> [!IMPORTANT]
>  应用 `<NetFx40_LegacySecurityPolicy>` 元素可能会导致由未在 [全局程序集缓存](../../../../../docs/framework/app-domains/gac.md) 中安装的 [本机映像生成器 \(Ngen.exe\)](../../../../../docs/framework/tools/ngen-exe-native-image-generator.md) 创建的本机映像程序集的性能严重下降。  应用该特性时，运行时无法将程序集作为本机映像加载会造成性能下降，从而导致他们将被作为实时程序集进行加载。  
  
> [!NOTE]
>  如果指定早于 Visual Studio 项目的项目设置中的 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 的目标 .NET Framework 版本，将会启用 CAS 策略，包括您为该版本指定的任何自定义 CAS 策略。  但您将无法使用新的 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 类型和成员。  也可以通过使用[application configuration file](../../../../../docs/framework/configure-apps/index.md)中的开始设置框架中的[\<supportedRuntime\> element](../../../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)来指定早期版本的 .NET Framework。  
  
> [!NOTE]
>  配置文件语法区分大小写。  应该以“语法”和“示例”部分所提供的那样使用语法。  
  
## 配置文件  
 此元素只可用于应用程序配置文件中。  
  
## 示例  
 下面的示例演示如何为某个应用程序启用旧版 CAS 策略。  
  
```  
<configuration>  
   <runtime>  
      <NetFx40_LegacySecurityPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)