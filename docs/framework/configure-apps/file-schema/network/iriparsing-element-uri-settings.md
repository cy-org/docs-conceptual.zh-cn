---
title: "&lt;iriParsing&gt; 元素（Uri 设置） | Microsoft Docs"
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
ms.assetid: 953d0b53-445e-41f9-b302-77c4030852ce
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# &lt;iriParsing&gt; 元素（Uri 设置）
指定是否对 <xref:System.Uri> 应用国际化资源标识符 \(IRI\) 分析以及是否应该应用 IRI 分析规则。  
  
## 架构层次结构  
 [\<configuration\> 元素](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<uri\> 元素（URI 设置）](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)  
  
 [\<iriParsing\>](../../../../../docs/framework/configure-apps/file-schema/network/iriparsing-element-uri-settings.md)  
  
## 语法  
  
```  
<idn  
  enabled="true|false"  
/idn>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|**元素**|**说明**|  
|------------|------------|  
|`enabled`|指定是否启用 IRI 分析。  默认值为 `false`。|  
  
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
  
2.  指定是否应启用 IRI 分析规则。  这可以在 machine.config 或 app.config 文件中完成。  
  
 启用 IRI 分析 \(iriParsing enabled \= `true`\) 将根据 RFC 3987 中的最新 IRI 规则执行规范化和字符检查。  默认值为 `false`，此时将根据 RFC 2396 和 RFC 3986（针对 IPv6 文本）执行规范化和字符检查。  
  
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
 <xref:System.Configuration.IriParsingElement?displayProperty=fullName>   
 <xref:System.Configuration.UriSection?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)