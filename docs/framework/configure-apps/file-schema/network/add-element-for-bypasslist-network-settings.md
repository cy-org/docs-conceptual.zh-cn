---
title: "bypasslist -&gt; &lt;add&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/add"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> 元素, bypasslist"
  - "<bypasslist>, add 元素"
  - "add 元素, bypasslist"
  - "bypasslist, add 元素"
ms.assetid: a0b86e28-86b4-4497-abe8-d5fd614c7926
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# bypasslist -&gt; &lt;add&gt; 元素（网络设置）
将 IP 地址或 DNS 名称添加到代理忽略列表中。  
  
## 语法  
  
```  
  
      <add   
   address = "regular expression"   
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|**address**|描述 IP 地址或 DNS 名称的正则表达式。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|提供一组正则表达式来描述不使用代理的地址。|  
  
## 备注  
 `add` 元素将描述 IP 地址或 DNS 服务器名称的正则表达式插入忽略代理服务器的地址的列表中。  
  
 `address` 特性的值应当是描述一组 IP 地址或主机名的一个正则表达式。  
  
 在为该元素指定正则表达式时应小心。  正则表达式“\[a\-z\]\+\\.contoso\\.com”不仅与 contoso.com 域中的任何主机匹配，而且还与 contoso.com.cpandl.com 域中的任何主机匹配。  若要仅与 contoso.com 域中的主机匹配，应使用定位点（“$”）：“\[a\-z\]\+\\.contoso\\.com$”。  
  
 有关正则表达式的更多信息，请参见 [.NET Framework 正则表达式](../../../../../docs/standard/base-types/regular-expressions.md)。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例向忽略列表添加两个地址。  第一个地址忽略 contoso.com 域中所有服务器的代理；第二个地址忽略 IP 地址以 192.168 开头的所有服务器的代理。  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <bypasslist>  
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