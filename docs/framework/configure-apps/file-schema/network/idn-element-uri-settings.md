---
title: "&lt;idn&gt; 元素（Uri 设置） | Microsoft Docs"
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
ms.assetid: 16c8e869-1791-4cf5-9244-3d3c738f60ec
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# &lt;idn&gt; 元素（Uri 设置）
指定是否对域名应用国际化域名 \(IDN\) 分析。  
  
## 架构层次结构  
 [\<configuration\> 元素](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<uri\> 元素（URI 设置）](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)  
  
 [\<idn\>](../../../../../docs/framework/configure-apps/file-schema/network/idn-element-uri-settings.md)  
  
## 语法  
  
```  
<idn  
  enabled="All|AllExceptIntranet|None"  
/idn>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|**元素**|**说明**|  
|------------|------------|  
|`enabled`|指定是否对域名应用国际化域名 \(IDN\) 分析，默认值为 none。|  
  
### 子元素  
 无  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[uri](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)|包含一些设置，用于指定 .NET Framework 如何处理使用统一资源标识符 \(URI\) 表示的 Web 地址。|  
  
## 备注  
 现有的 <xref:System.Uri> 类已在 .NET Framework 3.5 中进行了扩展。3.0 SP1 和支持国际资源标识符 \(IRI\) 和国际化域名 \(IDN\) 的 2.0 SP1。  当前用户将不会看到 .NET Framework 2.0 行为的任何变化，除非他们专门启用 IRI 和 IDN 支持。  这确保了应用程序与以前版本的 .NET Framework 的兼容性。  
  
 若要启用对 IRI 的支持，必须进行以下两项更改：  
  
1.  在 .NET Framework 2.0 目录下的 machine.config 文件中添加以下代码行  
  
    ```  
    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    ```  
  
2.  指定是否将国际化域名 \(IDN\) 语法分析应用于域名，以及是否需应用 IRI 语法分析规则。  这可以在 machine.config 或 app.config 文件中完成。  
  
 IDN 有三个可能的值，具体取决于所使用的 DNS 服务器：  
  
-   idn enabled \= All  
  
     此值会将所有 Unicode 域名转换为它们的 Punycode 等效项（IDN 名称）。  
  
-   idn enabled \= AllExceptIntranet  
  
     此值会将所有不在本地 Intranet 中的 Unicode 域名转换为使用 Punycode 等效项（IDN 名称）。  在这种情况下，若要处理本地 Intranet 上的国际化名称，用于 Intranet 的 DNS 服务器应该支持 Unicode 名称解析。  
  
-   idn enabled \= None  
  
     此值不会将任何 Unicode 域名转换为使用 Punycode。  这是与 .NET Framework 2.0 行为一致的默认值。  
  
 启用 IDN 会将域名中的所有 Unicode 标签转换为它们的 Punycode 等效项。  Punycode 名称仅包含 ASCII 字符，并且总是以 xn\-\- 前缀开头。  这样做是为了支持 Internet 中现有的 DNS 服务器，因为大多数 DNS 服务器仅支持 ASCII 字符（请参见 RFC 3940）。  
  
### 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
  
### 说明  
 下面的代码示例演示 <xref:System.Uri> 类为支持 IRI 分析和 IDN 名称所使用的配置。  
  
### 代码  
  
```  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
  </uri>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Configuration.IdnElement?displayProperty=fullName>   
 <xref:System.Configuration.UriSection?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)