---
title: "&lt;relativeBindForResources&gt; 元素 | Microsoft Docs"
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
  - "<relativeBindForResources> 元素"
  - "RelativeBindForResources 元素"
ms.assetid: 846ffa47-7257-4ce3-8cac-7ff627e0e34f
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;relativeBindForResources&gt; 元素
为附属程序集优化探查。  
  
## 语法  
  
```vb  
<relativeBindForResources    
   enabled="true|false" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定公共语言运行时是否为附属程序集优化探查。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|运行时不会为附属程序集优化探查。  这是默认值。|  
|`true`|运行时会为附属程序集优化探查。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含关于运行时初始化选项的信息。|  
  
## 备注  
 通常，资源管理器为资源进行探查，就像在[打包和部署资源](../../../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)主题中写下的文档。  这意味着当资源管理器为一个特定的本地化资源版本进行探查时，可能在全局程序集中查找，在应用程序的代码基中查找一个指定文化的目录，为附属程序集查找Windows安装器，引发<xref:System.AppDomain.AssemblyResolve?displayProperty=fullName>事件。  `<relativeBindForResources>`元素优化资源管理器为附属程序集进行探查的方式。  在接下来的情况下，它可以提高探查资源时的性能。  
  
-   当附属程序集在代码程序集相同的位置进行开展时。  换句话说，如果代码程序集被安装在全局程序集缓存，附属程序集必须被安装在这里。  代码程序集被安装在应用程序代码基，附属附属程序集必须被安装在代码基中的指定文化的文件夹。  
  
-   当 Windows Installer未使用或者只是很少的为附属程序集的按需安装使用。  
  
-   当应用程序代码不处理 <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> 事件。  
  
 将 `<relativeBindForResources>` 元素的 `enabled` 特性设置为 `true` 优化附属程序集中的资源管理器的探测如下：  
  
-   使用该父代码程序集的位置来进行附属程序集的探测。  
  
-   不查询附属程序集的 Windows Installer。  
  
-   这不会引发 <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> 事件。  
  
## 请参阅  
 [打包和部署资源](../../../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)   
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)