---
title: "&lt;uri&gt; 元素（URI 设置） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: c22bab8b-477c-4ae4-8498-65ad409e0847
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# &lt;uri&gt; 元素（URI 设置）
包含一些设置，用于指定 .NET Framework 如何处理使用统一资源标识符 \(URI\) 表示的 Web 地址。  
  
## 架构层次结构  
 [\<configuration\> 元素](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<uri\>](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)  
  
## 语法  
  
```  
<uri>  
</uri>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[idn enabled](../../../../../docs/framework/configure-apps/file-schema/network/idn-element-uri-settings.md)|指定是否对域名应用国际化域名 \(IDN\) 分析。|  
|[iriParsing](../../../../../docs/framework/configure-apps/file-schema/network/iriparsing-element-uri-settings.md)|指定是否对 <xref:System.Uri> 应用国际化资源标识符 \(IRI\) 分析以及是否应该应用 IRI 分析规则。|  
|[schemeSettings](../../../../../docs/framework/configure-apps/file-schema/network/schemesettings-element-uri-settings.md)|指定如何针对特定方案分析 <xref:System.Uri>。|  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[配置](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|包含所有命名空间的设置。|  
  
## 备注  
 `uri` 元素包含 <xref:System.Uri> 类的成员的设置，该类由 <xref:System.Net> 命名空间中的类使用。  这些设置配置对 IRI 和 IDN 支持。  
  
## 示例  
  
### 说明  
 下面的代码示例演示 <xref:System.Uri> 类为支持 IRI 分析和 IDN 名称所使用的配置。  此示例还会清除所有方案设置，然后添加对在 http 方案中不为使用百分号编码的路径分隔符进行转义的支持。  
  
### 代码  
  
```  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
    <schemeSettings>  
      <clear/>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## 请参阅  
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)