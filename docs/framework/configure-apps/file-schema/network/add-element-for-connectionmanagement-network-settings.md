---
title: "connectionManagement -&gt; &lt;add&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#add"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement/add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> 元素, connectionManagement"
  - "<connectionManagement>, add 元素"
  - "add 元素, connectionManagement"
  - "connectionManagement, add 元素"
ms.assetid: 856bf57d-1c63-46c7-a178-03d97b0a4149
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# connectionManagement -&gt; &lt;add&gt; 元素（网络设置）
将 IP 地址或 DNS 名称添加到连接管理列表。  
  
## 语法  
  
```  
  
        <add   
   address = "address expression"   
   maxconnection = integer   
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**描述**|  
|------------|------------|  
|`address`|描述 IP 地址或 DNS 名称的字符串。|  
|`maxconnection`|允许连接至服务器的最大连接数。  如果未提供，则默认为 2。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**描述**|  
|------------|------------|  
|[connectionManagement](../../../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)|指定到网络主机的最大连接数。|  
  
## 备注  
 `address` 特性的值应该是一个星号以指示所有连接，或为 `<schema>://<idn_hostname>[:<port>]` 格式的字符串。  
  
 如果传递到任何 HTTP API 的 URI 包含 Unicode，那么将使用 <xref:System.Uri.DnsSafeHost%2A> 内部转换名称，这可能会返回一个 punicode 字符串（行为取决于当前 IDN 配置）。  
  
## 配置文件  
 此元素可在应用程序配置文件或计算机配置文件 \(Machine.config\) 中使用。  
  
## 示例  
 下面的代码示例将应用程序配置为使用 4 个到 www.contoso.com 服务器的连接和 2 个到所有其他服务器的连接。  
  
```  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <add address = "http://www.contoso.com" maxconnection = "4" />  
      <add address = "*" maxconnection = "2" />  
    </connectionManagement>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.ServicePoint>   
 <xref:System.Net.ServicePointManager>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)