---
title: "bypasslist -&gt; &lt;remove&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/remove"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<bypasslist>, remove 元素"
  - "bypasslist, remove 元素"
  - "remove 元素, bypasslist"
  - "remove 元素, bypasslist"
ms.assetid: 61dcfb4a-e3d9-4abf-a2cd-7d685fe2f64b
caps.latest.revision: 16
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 16
---
# bypasslist -&gt; &lt;remove&gt; 元素（网络设置）
从代理忽略地址列表中移除 IP 地址或 DNS 名称。  
  
## 语法  
  
```  
  
      <remove   
   name = "regular expression"   
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|`name`|描述 IP 地址或 DNS 名称的正则表达式。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|提供一组正则表达式来描述不使用代理的地址。|  
  
## 备注  
 `remove` 元素将描述 IP 地址或 DNS 服务器名称的正则表达式从忽略代理服务器的地址的列表中移除。  这些地址是较早在配置文件中或在配置层次结构的较高级别定义的。  
  
 `name` 特性的值应当是描述一组 IP 地址或主机名的正则表达式。  
  
 有关正则表达式的更多信息，请参见 [.NET Framework 正则表达式](../../../../../docs/standard/base-types/regular-expressions.md)。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例移除 adventure\-works.com 域的所有以前的定义，然后将 contoso.com 域添加到忽略列表中。  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <bypasslist>  
        <remove name = "[a-z]+\.adventure-works\.com$" />  
        <add address="[a-z]+\.contoso\.com$" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.WebProxy?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)