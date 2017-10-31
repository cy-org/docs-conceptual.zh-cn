---
title: "webRequestModules -&gt; &lt;clear&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/clear"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#clear"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<clear> 元素, webRequestModules"
  - "<webRequestModules>, clear 元素"
  - "clear 元素, webRequestModules"
  - "webRequestModules, clear 元素"
ms.assetid: 48f38bcb-f30c-4b74-a8f0-1a3caf1aa96f
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# webRequestModules -&gt; &lt;clear&gt; 元素（网络设置）
从应用程序中移除所有已注册的 Web 请求模块。  
  
## 语法  
  
```  
  
<clear/>  
  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|指定用于向网络主机请求信息的模块。|  
  
## 备注  
 `clear` 元素移除所有注册的 Web 请求模块，这些请求模块是较早在配置文件中或在配置层次结构的较高级别定义的。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例清除所有 Web 请求模块，然后为 HTTP 注册 Web 请求模块。  
  
```  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <clear/>  
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