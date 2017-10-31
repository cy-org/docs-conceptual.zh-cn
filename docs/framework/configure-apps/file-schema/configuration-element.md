---
title: "&lt;configuration&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<configuration> 元素"
  - "配置元素"
  - "容器标记, <configuration> 元素"
ms.assetid: 2ec1c9dc-2e5c-4ef0-9958-81670ab88449
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# &lt;configuration&gt; 元素
公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。  
  
 **\<configuration（配置）\>**  
  
## 语法  
  
```  
  
      <configuration>   
   <!-- configuration settings -->   
</configuration>  
```  
  
## 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<assemblyBinding\> 元素](../../../../docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md)|指定配置级的程序集绑定策略。|  
|[启动设置架构](../../../../docs/framework/configure-apps/file-schema/startup/index.md)|启动设置架构中的所有元素。|  
|[运行时设置架构](../../../../docs/framework/configure-apps/file-schema/runtime/index.md)|运行时设置架构中的所有元素。|  
|[远程处理设置架构](http://msdn.microsoft.com/zh-cn/dc2d1e62-9af7-4ca1-99fd-98b93bb4db9e)|远程处理设置架构中的所有元素。|  
|[网络设置架构](../../../../docs/framework/configure-apps/file-schema/network/index.md)|网络设置架构中的所有元素。|  
|[加密设置架构](../../../../docs/framework/configure-apps/file-schema/cryptography/index.md)|加密设置架构中的所有元素。|  
|[配置节架构](../../../../docs/framework/configure-apps/file-schema/configuration-sections-schema.md)|配置节设置架构中的所有元素。|  
|[跟踪和调试设置架构](../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)|跟踪和调试设置架构中的所有元素。|  
|[ASP.NET 设置架构](http://msdn.microsoft.com/zh-cn/116608f3-c03d-4413-9fc7-978703e18b0f)|ASP.NET 配置架构中的所有元素，包括用于配置 ASP.NET 网站和应用程序的元素。  在 Web.config 文件中使用。|  
|[XML Web Services 设置架构](http://msdn.microsoft.com/zh-cn/f84d6d55-1add-4eb7-ae46-33df5833ea2e)|Web services 设置架构中的所有元素。|  
|[Web 设置架构](../../../../docs/framework/configure-apps/file-schema/web/index.md)|Web 设置架构中的所有元素，包括用于配置 ASP.NET 如何与宿主应用程序（如 IIS）一起工作的元素。  在 aspnet.config 文件中使用。|  
  
## 备注  
 每个配置文件必须准确包含一个**\<configuration\>**元素。  
  
## 请参阅  
 [配置文件架构](../../../../docs/framework/configure-apps/file-schema/index.md)