---
title: "&lt;proxy&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/proxy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#proxy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<proxy> 元素"
  - "proxy 元素"
ms.assetid: 37a548d8-fade-4ac5-82ec-b49b6c6cb22a
caps.latest.revision: 20
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 20
---
# &lt;proxy&gt; 元素（网络设置）
定义代理服务器。  
  
## 语法  
  
```  
  
      <proxy   
  autoDetect="true|false|unspecified"    
  bypassonlocal="true|false|unspecified"   
  proxyaddress="uriString"  
  scriptLocation="uriString"   
  usesystemdefault="true|false|unspecified "   
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|`autoDetect`|指定是否自动检测代理。  默认值为 `unspecified`。|  
|`bypassonlocal`|指定对于本地资源是否跳过代理。  本地资源包括本地服务器（http:\/\/localhost、http:\/\/loopback 或 http:\/\/127.0.0.1）和没有句点的 URI \(http:\/\/webserver\)。  默认值为 `unspecified`。|  
|`proxyaddress`|指定要使用的代理 URI。|  
|`scriptLocation`|指定配置脚本的位置。|  
|`usesystemdefault`|指定是否使用 Internet Explorer 代理设置。  如果设置为 `true`，则后面的特性将重写 Internet Explorer 代理设置。  默认值为 `unspecified`。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[defaultProxy](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|配置超文本传输协议 \(HTTP\) 代理服务器。|  
  
## 文本值  
  
## 备注  
 `proxy` 元素为应用程序定义代理服务器。  如果配置文件中缺少此元素，则 .NET Framework 将使用 Internet Explorer 中的代理设置。  
  
 `proxyaddress` 特性的值应当是格式良好的统一资源标识符 \(URI\)。  
  
 `scriptLocation` 特性引用代理自动检测配置脚本。  当在 Internet Explorer 中选中了**“使用自动配置脚本”**选项时，<xref:System.Net.WebProxy> 类将尝试定位配置脚本（其名称通常为 Wpad.dat）。  
  
 对于要迁移到 2.0 版的 .NET Framework 1.1 版应用程序，请使用 `usesystemdefault` 特性。  
  
 如果 `proxyaddress` 特性指定了无效的默认代理，则会引发异常。  该异常上的 <xref:System.Exception.InnerException%2A> 属性应该有关于错误根本原因的详细信息。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例使用 Internet Explorer 代理的默认设置，指定代理地址并对本地访问跳过代理。  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="true"  
      />  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.WebProxy?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)