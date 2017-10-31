---
title: "webRequestModules -&gt; &lt;remove&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/remove"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<remove> 元素, webRequestModules"
  - "<webRequestModules>, remove 元素"
  - "remove 元素, webRequestModules"
  - "webRequestModules, remove 元素"
ms.assetid: dd84d2fe-2f4f-457a-9d3c-441d0d21cc10
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# webRequestModules -&gt; &lt;remove&gt; 元素（网络设置）
从应用程序中移除自定义 Web 请求模块。  
  
## 语法  
  
```  
  
      <remove   
  name = "URI prefix"   
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|`name`|由该 Web 请求模块处理的请求的 URI 前缀。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|指定用于向网络主机请求信息的模块。|  
  
## 备注  
 `remove` 元素移除指定 URI 前缀的已注册 Web 请求模块。  
  
 `prefix` 特性的值应当是有效 URI 的前导字符，例如，“http”或“http:\/\/www.contoso.com”。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例移除 HTTP 的现有 Web 请求模块，然后为指向 www.contoso.com 的 HTTP 请求注册一个新的自定义 Web 请求模块。  
  
```  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <remove prefix = "http">  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator, System, Version=2.0.3600.0,  
           Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.WebRequest>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)