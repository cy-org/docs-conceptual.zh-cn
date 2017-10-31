---
title: "&lt;codeBase&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#codeBase"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/codeBase"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<codeBase> 元素"
  - "codeBase 元素"
  - "容器标记, <codeBase> 元素"
ms.assetid: d48a3983-2297-43ff-a14d-1f29d3995822
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# &lt;codeBase&gt; 元素
指定公共语言运行时可以在何处找到程序集。  
  
## 语法  
  
```  
  
   <codeBase    
version="Assembly version"  
href="URL of assembly"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`href`|必需的特性。<br /><br /> 指定运行时可在哪个 URL 处找到指定版本的程序集。|  
|`version`|必需的特性。<br /><br /> 指定基本代码适用于哪个程序集版本。  程序集版本号的格式是 *major.minor.build.revision*。|  
  
## version 特性  
  
|值|说明|  
|-------|--------|  
|版本号的每个部分的有效值为 0 到 65535。|不适用。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`buildproviders`|定义用于编译自定义资源文件的生成提供程序的集合。  您可以拥有任意数量的生成提供程序。|  
|`compilation`|配置 ASP.NET 使用的所有编译设置。|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`System.web`|为 ASP.NET 配置节指定根元素。|  
  
## 备注  
 为使运行时可在计算机配置文件或出版商策略文件中使用**\<codeBase\>** 设置，该文件还必须重定向程序集版本。  应用程序配置文件可在不重定向程序集版本的情况下拥有基本代码设置。  确定要使用的程序集版本后，运行时应用确定版本的文件中的基本代码设置。  如果未指示基本代码，运行时便以常用的方式寻找程序集。  
  
 如果程序集具有强名称，则基本代码设置可以是本地 Intranet 或 Internet 上的任何地方。  如果程序集为私有程序集，则基本代码设置必须是相对于应用程序目录的路径。  
  
 对于没有强名称的程序集，则忽略版本，并且加载程序使用\<codebase\> inside \<dependentAssembly\>内出现的第一个 \<codebase\>。  如果应用程序配置文件中具有将绑定重定向到另一个程序集的项，则即使该程序集版本与绑定请求不匹配，重定向仍具有优先权。  
  
## 示例  
 下面的示例说明如何指定运行时可在何处找到程序集。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <codeBase version="2.0.0.0"  
                      href="http://www.litwareinc.com/myAssembly.dll"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [指定程序集的位置](../../../../../docs/framework/configure-apps/specify-assembly-location.md)   
 [运行时如何定位程序集](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)