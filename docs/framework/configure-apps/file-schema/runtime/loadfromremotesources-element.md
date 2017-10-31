---
title: "&lt;loadFromRemoteSources&gt; 元素 | Microsoft Docs"
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
  - "loadFromRemoteSources 元素"
  - "<loadFromRemoteSources> 元素"
ms.assetid: 006d1280-2ac3-4db6-a984-a3d4e275046a
caps.latest.revision: 31
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 31
---
# &lt;loadFromRemoteSources&gt; 元素
指定来自远程源的程序集是否应授予完全信任。  
  
> [!NOTE]
>  如果由于 Visual Studio 项目错误列表中或生成错误中的错误消息，而定向到此主题，请参见[如何：在 Visual Studio 中使用 Web 上的程序集](http://msdn.microsoft.com/zh-cn/d8635b63-89a0-41aa-90f4-f351b2111070)。  
  
## 语法  
  
```  
<loadFromRemoteSources    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定加载自远程源的程序集是否应授予完全信任。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|不要向来自远程源的应用程序授予完全信任。  这是默认设置。|  
|`true`|向来自远程源的应用程序授予完全信任。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含关于运行时初始化选项的信息。|  
  
## 备注  
 在 .NET Framework 3.5 版本和早期版本中，如果从远程位置加载一个程序集，则该程序集将作为部分信任的程序集运行，并获得与其加载自的区域相关的授权集。  例如，加载自某个网站的程序集会加载到 Internet 区域中并被授予 Internet 权限集。  换言之，将在 Internet 沙盒中执行这些程序集。  如果尝试在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]和以后的版本中运行该程序集，会引发异常；必须为程序集\(参见[如何：运行沙盒中部分受信任的代码](../../../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)\)显式创建一个沙盒，或在完全信任环境下运行它。  
  
 利用 `<loadFromRemoteSources>` 元素，您可以指定在早期版本的 .NET Framework 中作为部分信任的程序集运行的程序集在  [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]和以后版本中作为完全信任的程序集运行。  默认情况下，远程程序集不在 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 和之后版本中运行。  若要运行远程的程序集，则运行为完全受信任或者创建运行它的沙盒<xref:System.AppDomain>。  
  
> [!NOTE]
>  在 [!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)]，则本地网络共享运行的程序集默认情况下作为完全信任；您不必启用 `<loadFromRemoteSources>` 元素。  
  
> [!NOTE]
>  如果应用程序已经从Web中复制，则它由 Windows 标记为 Web 应用程序，即使它驻留在本地计算机上。  通过更改文件属性，您可以更改该标记，也可以使用 `<loadFromRemoteSources>` 元素对程序集授予完全信任。  或者，可以使用 <xref:System.Reflection.Assembly.UnsafeLoadFrom%2A> 方法加载操作系统标记为从网站加载的本地的程序集。  
  
 此元素的 `enabled` 特性仅在禁用代码访问安全性 \(CAS\) 时有效。  默认情况下，[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 和更高版本中会禁用 CAS 策略。  如果将 `enabled` 设置为 `true`，则会将远程应用程序作为完全信任的应用程序运行。  
  
 如果未将 `<loadFromRemoteSources>` `enabled` 设置为 `true`，则在以下情况下会引发异常：  
  
-   当前域的沙盒行为与其在 [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)] 中的沙盒行为不同。  这要求禁用 CAS 策略，并且当前域不进行沙盒处理。  
  
-   所加载的程序集不是来自 `MyComputer` 区域。  
  
> [!NOTE]
>  当您尝试从承载计算机上的链接文件夹加载文件时，您可以在 Windows Virtual PC 应用程序中获取 <xref:System.IO.FileLoadException>。  此错误还可生成，则在尝试从[远程桌面服务](http://go.microsoft.com/fwlink/?LinkId=182775) \("终端服务\)上链接的文件夹加载文件时。  若要避免此异常，请将 `enabled` 设置为 `true`  
  
 将 `<loadFromRemoteSources>` 元素设置为 `true` 可防止出现此异常。  可利用此元素指定，您不依赖于公共语言运行时来对加载的程序集进行沙盒处理以确保安全，并指定可以将这些程序集作为完全信任的程序集运行。  
  
> [!IMPORTANT]
>  如果不应在完全信任环境下运行该程序集，请不要设置此配置元素，  而应创建一个在其中加载该程序集的沙盒化 <xref:System.AppDomain>。  
  
## 配置文件  
 此元素通常用在应用程序配置文件，则根据上下文可用在其他配置文件。  有关更多信息，请参见 .NET 安全的博客文章 [使用 CAS 策略的更隐式的使用：loadFromRemoteSources](http://go.microsoft.com/fwlink/p/?LinkId=266839)。  
  
## 示例  
 下面的示例演示如何从远程源对应用程序授予完全信任。  
  
```  
<configuration>  
   <runtime>  
      <loadFromRemoteSources enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [使用 CAS 策略的更隐式的使用：loadFromRemoteSources](http://go.microsoft.com/fwlink/p/?LinkId=266839)   
 [如何：运行沙盒中部分受信任的代码](../../../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)   
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)