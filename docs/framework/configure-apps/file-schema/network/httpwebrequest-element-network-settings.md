---
title: "&lt;httpWebRequest&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/httpWebRequest"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#httpWebRequest"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<httpWebRequest> 元素"
  - "httpWebRequest 元素"
ms.assetid: 52acd9d2-5bdc-4dc4-9c2a-f0a476ccbb31
caps.latest.revision: 18
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 18
---
# &lt;httpWebRequest&gt; 元素（网络设置）
自定义 Web 请求参数。  
  
## 语法  
  
```  
  
      <httpWebRequest  
  maximumResponseHeadersLength="size"  
  maximumErrorResponseLength="size"  
  maximumUnauthorizedUploadLength="size"  
  useUnsafeHeaderParsing="true|false"  
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|`maximumResponseHeadersLength`|指定响应标头的最大长度（以千字节为单位）。  默认值为 64。  值为 \-1 表示将不对响应标头的大小施加限制。|  
|`maximumErrorResponseLength`|指定错误响应的最大长度（以千字节为单位）。  默认值为 64。  值为 \-1 表示将不对错误响应的大小施加限制。|  
|`maximumUnauthorizedUploadLength`|指定用来响应未经授权的错误代码的上载的最大长度（以字节为单位）。  默认值为 \-1。  值 \-1 表示没有对上载施加大小限制。|  
|`useUnsafeHeaderParsing`|指定是否启用不安全的标头分析。  默认值为 `false`。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[设置](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|配置 <xref:System.Net> 命名空间的基本网络选项。|  
  
## 备注  
 默认情况下，.NET Framework 严格强制 URI 分析遵循 RFC 2616。  某些服务器响应可能在禁用字段中包括控制字符，这会导致 <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=fullName> 方法引发 <xref:System.Net.WebException>。  如果 **useUnsafeHeaderParsing** 设置为 **true**，在这种情况下 <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=fullName> 将不会引发异常；但是，应用程序将易于受到几种形式的 URI 分析攻击的侵害。  最佳解决方案是更改服务器，以便在响应中不包括控制字符。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例演示如何指定一个大于正常最大标头长度的长度值。  
  
```  
<configuration>  
  <system.net>  
    <settings>  
      <httpWebRequest  
        maximumResponseHeadersLength="128"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)