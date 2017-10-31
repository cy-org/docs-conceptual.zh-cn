---
title: "&lt;defaultProxy&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultProxy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<defaultProxy> 元素"
  - "defaultProxy 元素"
ms.assetid: 9d663c4b-07b4-4f6f-9b12-efbd3630354f
caps.latest.revision: 21
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 21
---
# &lt;defaultProxy&gt; 元素（网络设置）
配置超文本传输协议 \(HTTP\) 代理服务器。  
  
## 语法  
  
```  
  
        <defaultProxy  
  enabled="true|false"  
  useDefaultCredentials="true|false"  
  <bypasslist> … </bypasslist>  
  <proxy> … </proxy>  
  <module> … </module>  
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|**元素**|**描述**|  
|------------|------------|  
|`enabled`|指定是否使用 Web 代理。  默认值为 `true`。|  
|`useDefaultCredentials`|指定是否使用此主机的默认凭据来访问 Web 代理。  默认值为 `false`。|  
  
### 子元素  
  
|**元素**|**描述**|  
|------------|------------|  
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|提供一组描述不使用代理的地址的正则表达式。|  
|[Module — 模块](../../../../../docs/framework/configure-apps/file-schema/network/module-element-network-settings.md)|向应用程序添加新的代理模块。|  
|[代理](../../../../../docs/framework/configure-apps/file-schema/network/proxy-element-network-settings.md)|定义代理服务器。|  
  
### 父元素  
  
|**元素**|**描述**|  
|------------|------------|  
|[system。  net](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|包含指定 .NET Framework 如何连接到网络的设置。|  
  
## 备注  
 如果 defaultProxy 元素为空，则将沿用 Internet Explorer 中的代理设置。  这种行为在 .NET Framework 1.1 版中有所不同。  
  
 如果 [module](../../../../../docs/framework/configure-apps/file-schema/network/module-element-network-settings.md) 元素指定非公共类型，该类型不派生自 <xref:System.Net.IWebProxy> 类，此对象的默认构造函数出现异常，或者检索系统指定的默认代理时发生了异常，则会引发异常。  异常的 <xref:System.Exception.InnerException%2A> 属性应具有错误根本原因的详细信息。  
  
## 配置文件  
 此元素可在应用程序配置文件或计算机配置文件 \(Machine.config\) 中使用。  
  
## 示例  
 下面的代码示例使用来自 Internet Explorer 代理的默认值，指定代理地址，并且在进行本地访问和访问 contoso.com 时不使用代理。  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="true"  
      />  
      <bypasslist  
        <add address="[a-z]+\.contoso\.com" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.WebProxy?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)