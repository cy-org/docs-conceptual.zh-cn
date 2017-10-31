---
title: "connectionManagement -&gt; &lt;remove&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement/remove"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<connectionManagement>, remove 元素"
  - "<remove> 元素, connectionManagement"
  - "connectionManagement, remove 元素"
  - "remove 元素, connectionManagement"
ms.assetid: 94b81775-5a22-4975-8c47-8620c40c3f35
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# connectionManagement -&gt; &lt;remove&gt; 元素（网络设置）
将 IP 地址或 DNS 名称从连接管理列表中移除。  
  
## 语法  
  
```  
  
      <remove   
   name = "server name or IP address"   
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|`address`|IP 地址或 DNS 名称。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[connectionManagement](../../../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)|指定与网络主机的最大连接数。|  
  
## 备注  
 `remove` 元素移除指定服务器的连接管理列表项。  
  
 `address` 特性的值应是有效的 IP 地址或主机名。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例移除服务器 www.adventure\-works.com 的所有连接管理列表项，然后将应用程序配置为使用四个与服务器 www.contoso.com 的连接和两个与其他所有服务器的连接。  
  
```  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <remove address = "http://www.adventure-works.com"/>  
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