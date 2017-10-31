---
title: "&lt;servicePointManager&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#servicePointManager"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/servicePointManager"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<servicePointManager> 元素"
  - "servicePointManager 元素"
ms.assetid: 6e5def51-3646-4ef6-a7bd-c69151321bec
caps.latest.revision: 16
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 16
---
# &lt;servicePointManager&gt; 元素（网络设置）
配置与网络资源的连接。  
  
## 语法  
  
```  
  
      <servicePointManager  
  checkCertificateName="true|false"  
  checkCertificateRevocationList="true|false"  
  encryptionPolicy="AllowNoEncryption|NoEncryption|RequireEncryption"  
  expect100Continue="true|false"  
  useNagleAlgorithm="true|false"  
  enableDnsRoundRobin="true|false"  
  dnsRefreshTimeout="time"  
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|`checkCertificateName`|指定系统在使用某个证书之前，是否应验证该证书上的名称是否与服务器主机名一致。  默认值为 `true`。|  
|`checkCertificateRevocationList`|指定系统在使用某个证书之前，是否应检查该证书是否已被吊销。  默认值为 `false`。|  
|`dnsRefreshTimeout`|指定当与“DNS 循环”选项结合使用时，域名服务 \(DNS\) 解析的缓存时间（以毫秒为单位）。  默认值是 120,000 毫秒（2 分钟）。|  
|`enableDnsRoundRobin`|指定在对具有多个 Internet 协议 \(IP\) 地址的主机名进行 DNS 解析时，是返回所有的地址还是只返回第一个地址。  默认值为 `false`。|  
|`encryptionPolicy`|指定应用于 <xref:System.Net.ServicePointManager> 实例上的 SSL\/TLS 会话的加密策略。  可能的值与 <xref:System.Net.Security.EncryptionPolicy> 枚举的值等效。  将加密策略设置为 `NoEncryption` 时，要求使用 <xref:System.Security.Authentication.CipherAlgorithmType>。  默认值为 `RequireEncryption`。|  
|`expect100Continue`|指定 POST 方法是否应当要求从服务器接收 `100-continue` 响应。  默认值为 `true`。|  
|`useNagleAlgorithm`|指定由服务点管理器控制的连接是否使用 Nagle 算法。  默认值为 `true`。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[设置](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|配置 <xref:System.Net> 命名空间的基本网络选项。|  
  
## 备注  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 请参阅  
 <xref:System.Net.ServicePointManager>   
 <xref:System.Net.Security.EncryptionPolicy>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)