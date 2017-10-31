---
title: "connectionManagement -&gt; &lt;clear&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement/clear"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#clear"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<clear> 元素, connectionManagement"
  - "<connectionManagement>, clear 元素"
  - "clear 元素, connectionManagement"
  - "connectionManagement, clear 元素"
ms.assetid: fb259282-84c4-4dc4-a226-78d904a6edc3
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# connectionManagement -&gt; &lt;clear&gt; 元素（网络设置）
清除连接管理列表。  
  
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
|[connectionManagement](../../../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)|指定与网络主机的最大连接数。|  
  
## 备注  
 `clear` 元素清除连接管理列表中的所有项。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例清除连接管理列表，然后为服务器 www.contoso.com 和其他所有网络主机添加新的连接管理项。  
  
```  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <clear/>  
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