---
title: "webRequestModules -&gt; &lt;add&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/add"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> 元素, webRequestModules"
  - "<webRequestModules>, add 元素"
  - "add 元素, webRequestModules"
  - "webRequestModules, add 元素"
ms.assetid: 47ec4adc-f39f-4bcd-8680-1ec21fd26890
caps.latest.revision: 16
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 16
---
# webRequestModules -&gt; &lt;add&gt; 元素（网络设置）
将自定义 Web 请求模块添加到应用程序。  
  
## 语法  
  
```  
  
      <add   
  prefix = "URI prefix"   
  type = "module name, Version, Culture, PublicKeyToken"   
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|`prefix`|由该 Web 请求模块处理的请求的 URI 前缀。|  
|`type`|实现该 Web 请求模块的模块的程序集和类名。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|指定用于向网络主机请求信息的模块。|  
  
## 备注  
 `prefix` 特性定义使用指定的 Web 请求模块的 URI 前缀。  Web 请求模块通常被注册来处理特定的协议（例如 HTTP 或 FTP），但也可能被注册来处理对特定服务器或服务器上的路径的请求。  
  
 在将 URI 匹配前缀传递给 <xref:System.Net.WebRequest.Create%2A?displayProperty=fullName> 方法时，会创建 Web 请求模块。  
  
 `prefix` 特性的值应当是有效 URI 的前导字符，例如，“http”或“http:\/\/www.contoso.com”。  
  
 `type` 特性的值应当是有效的 DLL 名称和对应的类名，二者之间用逗号分隔。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例为 HTTP 注册自定义 Web 请求模块。  应当将 Version 和 PublicKeyToken 的值替换为指定模块的正确值。  
  
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
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)