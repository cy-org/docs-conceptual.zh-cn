---
title: "&lt;developmentMode&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/developmentMode"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#developmentMode"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<developmentMode> 元素"
  - "容器标记, <developmentMode> 元素"
  - "developmentMode 元素"
ms.assetid: 60e79a8c-415a-497d-be29-b9d0fd9bdee3
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# &lt;developmentMode&gt; 元素
指定运行时是否在 DEVPATH 环境变量指定的目录中搜索程序集。  
  
## 语法  
  
```  
<developmentMode developerInstallation="true | false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|**developerInstallation**|指定运行时是否在 DEVPATH 环境变量指定的目录中搜索程序集。|  
  
## developerInstallation 特性  
  
|值|说明|  
|-------|--------|  
|**true**|在 DEVPATH 环境变量指定的目录中搜索程序集。|  
|**false**|不在 DEVPATH 环境变量指定的目录中搜索程序集。  此为默认值。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 仅在开发时使用此设置。  运行时不检查在 DEVPATH 中找到的具有强名称的程序集的版本。  它只是使用所找到的第一个程序集。  
  
## 示例  
 下面的示例说明如何使运行时在由 DEVPATH 环境变量所指定的目录中搜索程序集。  
  
```  
<configuration>  
   <runtime>  
      <developmentMode developerInstallation="true"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [如何：使用 DEVPATH 查找程序集](../../../../../docs/framework/configure-apps/how-to-locate-assemblies-by-using-devpath.md)