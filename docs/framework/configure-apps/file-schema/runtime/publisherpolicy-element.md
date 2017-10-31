---
title: "&lt;publisherPolicy&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/publisherPolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/publisherPolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#publisherPolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<publisherPolicy> 元素"
  - "容器标记, <publisherPolicy> 元素"
  - "publisherPolicy 元素"
ms.assetid: 4613407e-d0a8-4ef2-9f81-a6acb9fdc7d4
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# &lt;publisherPolicy&gt; 元素
指定运行时是否采用出版商策略。  
  
## 语法  
  
```  
  
<publisherPolicy apply="yes|no"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`apply`|指定是否应用出版商策略。|  
  
## 应用特性  
  
|值|说明|  
|-------|--------|  
|`yes`|应用出版商策略。  此设置为默认设置。|  
|`no`|不应用出版商策略。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 当组件供应商发布新版本的程序集时，供应商可以包含出版商策略，以便使用旧版本的应用程序现在使用新版本。  为了指定是否为一个特定的程序集使用出版商策略，把**\<publisherPolicy\>**元素放入**\<dependentAssembly\>**元素。  
  
 **apply** 特性的默认设置为 **yes**。  将 **apply** 特性设置为 **no** 会重写程序集任何以前的 **yes** 设置。  
  
 应用程序需要一个权限通过使用应用程序配置文件中[\<publisherPolicy apply\="no"\/\>](../../../../../docs/framework/configure-apps/file-schema/runtime/publisherpolicy-element.md)元素来显式地忽略版权政策。  该权限可通过针对 [SecurityPermission Class](frlrfSystemSecurityPermissionsSecurityPermissionClassTopic)设置  [BindingRedirects](frlrfSystemSecurityPermissionsSecurityPermissionFlagClassTopic)标志来授予。  有关更多信息，请参见[程序集绑定重定向安全权限](../../../../../docs/framework/configure-apps/assembly-binding-redirection-security-permission.md)。  
  
## 示例  
 下面的示例为程序集 `myAssembly` 关闭了出版商策略。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                                    publicKeyToken="32ab4ba45e0a69a1"  
                                    culture="neutral" />  
            <publisherPolicy apply="no"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [运行时如何定位程序集](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [重定向程序集版本](../../../../../docs/framework/configure-apps/redirect-assembly-versions.md)