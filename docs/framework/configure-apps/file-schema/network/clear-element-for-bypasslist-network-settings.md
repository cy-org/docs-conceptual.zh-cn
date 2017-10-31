---
title: "bypasslist -&gt; &lt;clear&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/clear"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#clear"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<bypasslist>, clear 元素"
  - "<clear> 元素, bypasslist"
  - "bypasslist, clear 元素"
  - "clear 元素, bypasslist"
ms.assetid: 301584ca-a914-4100-b180-3b288d3b099e
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# bypasslist -&gt; &lt;clear&gt; 元素（网络设置）
清除代理忽略列表。  
  
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
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|提供一组正则表达式来描述不使用代理的地址。|  
  
## 备注  
 `clear` 元素清除忽略列表中的所有项。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例清除忽略列表，然后向该忽略列表添加两个地址。  第一个地址忽略 contoso.com 域中所有服务器的代理；第二个地址忽略 IP 地址以 192.168 开头的所有服务器的代理。  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <bypasslist>  
         <clear/>  
        <add address="[a-z]+\.contoso\.com$" />  
        <add address="192\.168\.\d{1,3}\.\d{1,3}" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>   
```  
  
## 请参阅  
 <xref:System.Net.WebProxy?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)