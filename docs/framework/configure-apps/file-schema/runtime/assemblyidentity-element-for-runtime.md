---
title: "&lt;runtime&gt; 的 &lt;assemblyIdentity&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/assemblyIdentity"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#assemblyIdentity"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<assemblyIdentity> 元素"
  - "assemblyIdentity 元素"
  - "容器标记, <assemblyIdentity> 元素"
ms.assetid: cea4d187-6398-4da4-af09-c1abc6a349c1
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# &lt;runtime&gt; 的 &lt;assemblyIdentity&gt; 元素
包含关于该程序集的标识信息。  
  
## 语法  
  
```  
  
   <assemblyIdentity    
name="assembly name"  
publicKeyToken="public key token"  
culture="assembly culture"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`name`|必需的特性。<br /><br /> 程序集的名称|  
|`culture`|可选特性。<br /><br /> 指定程序集的语言和国家\/地区的字符串。|  
|`publicKeyToken`|可选特性。<br /><br /> 指定程序集强名称的十六进制值。|  
|`processorArchitecture`|可选特性。<br /><br /> “x86”、“amd64”、“msil”或“ia64”值之一，为包含特定于处理器的代码的程序集指定处理器架构。  这些值不区分大小写。  如果该特性被赋予任何其他值，则整个 `<assemblyIdentity>` 元素将被忽略。  请参见<xref:System.Reflection.ProcessorArchitecture>。|  
  
## processorArchitecture 特性  
  
|值|说明|  
|-------|--------|  
|`amd64`|仅 64 位 AMD 处理器。|  
|`ia64`|仅 64 位 Intel 处理器。|  
|`msil`|不特定于处理器和每字位数|  
|`x86`|32 位 Intel 处理器，位于本机上或位于 64 位平台上的 Windows on Windows \(WOW\) 环境中。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`assemblyBinding`|包含有关程序集版本重定向和程序集位置的信息。|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`dependentAssembly`|封装每个程序集的绑定策略和程序集位置。  为每个程序集使用一个 `<dependentAssembly>` 元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 每个 **\<dependentAssembly\>**元素都必须有一个**\<assemblyIdentity\>** 子元素。  
  
 如果存在 `processorArchitecture` 特性，则 `<assemblyIdentity>` 元素仅应用于具有相应处理器架构的程序集。  如果不存在 `processorArchitecture` 特性，则 `<assemblyIdentity>` 元素可以应用于具有任何处理器架构的程序集。  
  
 下面的示例演示一个配置文件用于两个名称相同的程序集，它们将两个不同的处理器架构作为目标，而且版本没有同步。  当应用程序在 x86 平台上执行时，第一个 `<assemblyIdentity>` 元素得到应用，而另一个被忽略。  如果应用程序在 x86 或 ia64 以外的其他平台上执行，两个元素都将被忽略。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"  
                  processorArchitecture="x86" />  
            <bindingRedirect oldVersion= "1.0.0.0"   
                  newVersion="1.1.0.0" />  
         </dependentAssembly>  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"   
                  processorArchitecture="ia64" />  
            <bindingRedirect oldVersion="1.0.0.0"   
                  newVersion="2.0.0.0" />  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 如果配置文件包含一个没有 `processorArchitecture` 特性的 `<assemblyIdentity>` 元素，并且不包含与平台匹配的元素，则将使用没有 `processorArchitecture` 特性的元素。  
  
## 示例  
 下面的示例说明如何提供有关程序集的信息。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <!--Redirection and codeBase policy for myAssembly.-->  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [重定向程序集版本](../../../../../docs/framework/configure-apps/redirect-assembly-versions.md)