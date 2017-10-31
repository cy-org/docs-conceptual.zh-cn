---
title: "&lt;webRequestModules&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#webRequestModules"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<webRequestModules> 元素"
  - "webRequestModules 元素"
ms.assetid: 1263de11-3e0a-4f94-97c9-710b2ae53817
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# &lt;webRequestModules&gt; 元素（网络设置）
指定用于向网络主机请求信息的模块。  
  
## 语法  
  
```  
  
      <webRequestModules>   
</webRequestModules>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[添加](../../../../../docs/framework/configure-apps/file-schema/network/add-element-for-webrequestmodules-network-settings.md)|将自定义 Web 请求模块添加到应用程序。|  
|[clear](../../../../../docs/framework/configure-apps/file-schema/network/clear-element-for-webrequestmodules-network-settings.md)|从应用程序中移除所有已注册的 Web 请求模块。|  
|[remove](../../../../../docs/framework/configure-apps/file-schema/network/remove-element-for-webrequestmodules-network-settings.md)|从应用程序中移除自定义 Web 请求模块。|  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[system.net](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|包含指定 .NET Framework 与网络的连接方式的设置。|  
  
## 备注  
 此`webRequestModules` 元素注册<xref:System.Net.WebRequest>类的子代，以处理向网络主机发出的信息请求。  Web 请求模块必须实现 <xref:System.Net.IWebRequestCreate> 接口。  
  
 .NET Framework 包括以 http:\/\/、https:\/\/ 和 file:\/\/ 起始的 URI 的 Web 请求模块。  只能通过在配置文件中注册自定义模块来重写默认模块。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例注册默认的 HTTP 模块。  应当将 Version 和 PublicKeyToken 的值替换为指定模块的正确值。  
  
```  
<configuration>  
  <system.net>  
    <webRequestModules>  
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
 <xref:System.Net.IWebRequestCreate>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)