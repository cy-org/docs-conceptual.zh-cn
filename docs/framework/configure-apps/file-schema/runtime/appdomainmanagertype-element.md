---
title: "&lt;appDomainManagerType&gt; 元素 | Microsoft Docs"
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
  - "<appDomainManagerType> 元素"
  - "appDomainManagerType 元素"
ms.assetid: ae8d5a7e-e7f7-47f7-98d9-455cc243a322
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;appDomainManagerType&gt; 元素
指定用作默认应用程序域的应用程序域管理器的类型。  
  
## 语法  
  
```  
<appDomainManagerAssembly   
   value="type name" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`value`|必需的特性。  指定用作进程内默认应用程序域的应用程序域管理器的类型的名称（包括命名空间）。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 若要指定应用程序域管理器的类型，必须同时指定此元素和 [\<appDomainManagerAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md)元素。  如果二者中的某个元素未指定，则另一个元素将被忽略。  
  
 在加载默认应用程序域时，如果指定的类型在[\<appDomainManagerAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md) 元素指定的程序集中不存在，则将引发 <xref:System.TypeLoadException>，并且无法启动进程。  
  
 在指定默认应用程序域的应用程序域管理器类型时，从默认应用程序域创建的其他应用程序域会继承应用程序域管理器类型。  使用 <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=fullName> 和 <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=fullName> 属性可以为新的应用程序域指定一个不同的应用程序域管理器类型。  
  
 指定应用程序域管理器类型要求应用程序受到完全信任。（例如，在桌面上运行的应用程序受到完全信任。）如果应用程序未受到完全信任，则将引发 <xref:System.TypeLoadException>。  
  
 类型和命名空间的格式与用于 <xref:System.Type.FullName%2A?displayProperty=fullName> 属性的格式相同。  
  
 此配置元素仅在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]和更高版本中可用。  
  
## 示例  
 下面的示例演示如何指定一个进程的默认应用程序域的应用程序域管理器是 `AdMgrExample` 程序集中的 `MyMgr` 类型。  
  
```  
<configuration>  
   <runtime>  
      <appDomainManagerType value="MyMgr" />  
      <appDomainManagerAssembly   
         value="AdMgrExample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=6856bccf150f00b3" />  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=fullName>   
 <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=fullName>   
 [\<appDomainManagerAssembly\> 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md)   
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [SetAppDomainManagerType 方法](../Topic/ICLRControl::SetAppDomainManagerType%20Method.md)