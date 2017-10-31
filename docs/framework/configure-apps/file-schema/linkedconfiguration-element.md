---
title: "&lt;linkedConfiguration&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/assemblyBinding/linkedConfiguration"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#linkedConfiguration"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<linkedConfiguration> 元素"
  - "配置文件 [.NET Framework], 链接的配置文件"
  - "包括配置文件"
  - "链接的配置文件"
  - "linkedConfiguration 元素"
ms.assetid: 8eb34f3b-427e-4288-a7ff-c73f489deb45
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# &lt;linkedConfiguration&gt; 元素
指定要包含的配置文件。  
  
## 语法  
  
```  
<linkedConfiguration  
   href="URL of linked configuration file"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`href`|要包含的配置文件的 URL。  唯一支持的 `href` 特性格式为“file:\/\/”。  支持本地文件和 UNC 文件。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<assemblyBinding\> 元素](../../../../docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md)|指定配置级的程序集绑定策略。|  
  
## 备注  
 `<linkedConfiguration>` 元素简化了为组件程序集提供的服务。  如果一个或多个应用程序使用的程序集有驻留在已知位置的配置文件，则使用该程序集的应用程序的配置文件可以使用 `<linkedConfiguration>` 元素来包含程序集配置文件，而不是直接包含配置信息。  向组件程序集提供服务后，更新公共配置文件将向使用该程序集的所有应用程序提供更新的配置信息。  
  
> [!NOTE]
>  具有 Windows 并行清单的应用程序不支持 `<linkedConfiguration>` 元素。  
  
 下面这些规则控制着链接配置文件的使用。  
  
-   所含配置文件中的设置仅影响加载程序绑定策略并仅由加载程序使用。  所含配置文件可以有绑定策略以外的其他设置，但这些设置不会有任何效果。  
  
-   唯一支持的 `href` 特性格式为“file:\/\/”。  支持本地文件和 UNC 文件。  
  
-   每个配置文件的链接配置数没有限制。  
  
-   所有链接配置文件都合并构成一个文件，与 C\/C\+\+ 中的 `#include` 指令行为类似。  
  
-   仅在应用程序配置文件中允许 `<linkedConfiguration>` 元素，在 Machine.config 中将忽略该元素。  
  
-   检测到循环引用并已将其终止。  即，如果一系列配置文件的 `<linkedConfiguration>` 元素组成一个循环，将检测到该循环并使其停止。  
  
## 示例  
 下面的代码示例演示如何包含本地硬盘的配置文件。  
  
```  
<configuration>  
   <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
      <linkedConfiguration href="file://c:\Program Files\Contoso\sharedConfig.xml"/>  
   </assemblyBinding>  
</configuration>  
```  
  
## 请参阅  
 [\<assemblyBinding\> 元素](../../../../docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md)   
 [配置文件架构](../../../../docs/framework/configure-apps/file-schema/index.md)