---
title: "&lt;runtime&gt; 的 &lt;assemblyBinding&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<assemblyBinding> 元素"
  - "assemblyBinding 元素"
  - "容器标记, <assemblyBinding> 元素"
ms.assetid: 964cbb35-ab49-4498-8471-209689e5dada
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# &lt;runtime&gt; 的 &lt;assemblyBinding&gt; 元素
包含有关程序集版本重定向和程序集位置的信息。  
  
## 语法  
  
```  
  
        <assemblyBinding    
   xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
</assemblyBinding>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|**xmlns**|必需的特性。<br /><br /> 指定程序集绑定所需的 XML 命名空间。  使用字符串“urn: 架构\-microsoft\-com:asm.v1”作为值。|  
|**appliesTo**|指定 .NET Framework 程序集重定向适用的运行时版本。  此可选特性用 .NET Framework 版本号来指示其适用的版本。  如果没有指定 **appliesTo** 特性，**\<assemblyBinding\>** 元素将适用于 .NET Framework 的所有版本。  **appliesTo** 特性是在 .NET Framework 1.1 版中引入的；.NET Framework 1.0 版将忽略该特性。  这意味着，即使指定了 **appliesTo** 特性，在使用 .NET Framework 1.0 版时所有的 **\<assemblyBinding\>** 元素也都适用。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<dependentAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/dependentassembly-element.md)|封装程序集的绑定策略和程序集位置。  为每个程序集使用一个 **\<dependentAssembly\>** 标记。|  
|[\<probing\>](../../../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md)|指定加载程序集时公共语言运行时搜索的子目录。|  
|[\<publisherPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/publisherpolicy-element.md)|指定运行时是否使用发布者策略。|  
|[\<qualifyAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/qualifyassembly-element.md)|指定使用部分名称时应动态加载的程序集全名。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 示例  
 下面的示例显示如何将一个程序集版本重定向到另一个版本并提供基本代码。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
            <codeBase version="2.0.0.0"  
                      href="http://www.litwareinc.com/myAssembly.dll"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 下面的示例显示如何使用 **appliesTo** 属性重定向 .NET Framework 程序集绑定。  
  
```  
<runtime>  
   <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
      <dependentAssembly>   
         <assemblyIdentity name="mscorcfg" publicKeyToken="b03f5f7f11d50a3a" culture=""/>  
         <bindingRedirect oldVersion="0.0.0.0-65535.65535.65535.65535" newVersion="1.0.3300.0"/>  
      </dependentAssembly>  
   </assemblyBinding>  
</runtime>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [重定向程序集版本](../../../../../docs/framework/configure-apps/redirect-assembly-versions.md)