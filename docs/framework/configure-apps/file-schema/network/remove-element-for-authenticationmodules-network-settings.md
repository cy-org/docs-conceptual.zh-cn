---
title: "authenticationModules -&gt; &lt;remove&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/authenticationModules/remove"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<authenticationModules>, remove 元素"
  - "<remove> 元素, authenticationModules"
  - "authenticationModules, remove 元素"
  - "remove 元素, authenticationModules"
ms.assetid: abf79949-b05c-465a-b51c-bbeda9a74173
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# authenticationModules -&gt; &lt;remove&gt; 元素（网络设置）
从应用程序中移除身份验证模块。  
  
## 语法  
  
```  
  
      <remove   
   name = "authentication module name"   
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|**name**|要移除的身份验证模块的名称。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[授权组件](../../../../../docs/framework/configure-apps/file-schema/network/authenticationmodules-element-network-settings.md)|指定用于对网络请求进行身份验证的模块。|  
  
## 备注  
 `remove` 元素移除身份验证模块，这些身份验证模块是较早在配置文件中或在配置层次结构的较高级别定义的。  
  
 `name` 特性的值应当是有效的类名。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例移除一个身份验证模块。  
  
```  
<configuration>  
  <system.net>  
    <authenticationModules>  
      <remove name = "System.Net.NtlmClient" />  
    </authenticationModules>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.IAuthenticationModule>   
 <xref:System.Net.AuthenticationManager>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)