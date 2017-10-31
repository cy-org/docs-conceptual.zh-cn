---
title: "&lt;qualifyAssembly&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#qualifyAssembly"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/qualifyAssembly"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<qualifyAssembly> 元素"
  - "容器标记, <qualifyAssembly> 元素"
  - "qualifyAssembly 元素"
ms.assetid: ad6442f6-1a9d-43b6-b733-04ac1b7f9b82
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# &lt;qualifyAssembly&gt; 元素
指定当使用程序集的部分名称时应动态加载的程序集全名。  
  
## 语法  
  
```  
  
      <qualifyAssembly partialName=  
      "PartialAssemblyName"  
                 fullName="FullAssemblyName"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`partialName`|必需的特性。<br /><br /> 指定在代码中出现的程序集的部分名称。|  
|`fullName`|必需的特性。<br /><br /> 指定在全局程序集缓存中出现的程序集的全名。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`assemblyBinding`|包含有关程序集版本重定向和程序集位置的信息。|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 如果使用程序集的部分名称调用 <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> 方法，则会导致公共语言运行时只在应用程序的基目录中查找程序集。  在应用程序的配置文件中使用**\<qualifyAssembly\>**元素可提供程序集的全部信息（名称、版本、公钥标记和区域性），使公共语言运行时在全局程序集缓存中搜索程序集。  
  
 **fullName** 特性必须包括程序集标识的四个字段：名称、版本、公钥标记和区域性。  **partialName** 特性必须部分地引用程序集。  必须至少指定程序集的文本名称（最常见的情况），但也可以包括版本、公钥标记或区域性（或者四个字段的任意组合，但不能包括全部四个）。  **partialName** 必须与调用中指定的名称匹配。  例如，不能在配置文件中将 `"math"` 指定为 **partialName** 特性，而在代码中调用 `Assembly.Load("math, Version=3.3.3.3")`。  
  
## 示例  
 下面的示例逻辑上将 `Assembly.Load("math")`  调用变成 `Assembly.Load("math,version=1.0.0.0,publicKeyToken=a1690a5ea44bab32,culture=neutral")`。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <qualifyAssembly partialName="math"   
                         fullName=  
"math,version=1.0.0.0,publicKeyToken=a1690a5ea44bab32,culture=neutral"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [运行时如何定位程序集](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [NIB: Partial Assembly References](http://msdn.microsoft.com/zh-cn/ec90f07a-398c-4306-9401-0fc5ff9cb59f)