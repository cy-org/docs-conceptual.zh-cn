---
title: "schemeSettings 的 &lt;clear&gt; 元素（Uri 设置） | Microsoft Docs"
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
ms.assetid: 65098332-ce61-4542-ab8d-e7dc0257d31f
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# schemeSettings 的 &lt;clear&gt; 元素（Uri 设置）
清除所有现有的方案设置。  
  
## 语法  
  
```  
  
<clear/>  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<schemeSettings\> 元素（Uri 设置）](../../../../../docs/framework/configure-apps/file-schema/network/schemesettings-element-uri-settings.md)|指定如何针对特定方案分析 <xref:System.Uri>。|  
  
## 备注  
 默认情况下，在执行路径压缩前，<xref:System.Uri?displayProperty=fullName> 类将取消转义百分号编码的路径分隔符。  这实现为抵御类似于如下攻击的安全机制：  
  
 `http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 如果在未正确处理百分号编码的字符的情况下将此 URI 传递给模块，可能会导致服务器执行下面的命令：  
  
 `c:\Windows\System32\cmd.exe /c dir c:\`  
  
 因此，<xref:System.Uri?displayProperty=fullName> 类首先取消转义路径分隔符，然后再应用路径压缩。  将上面的恶意 URL 传递给 <xref:System.Uri?displayProperty=fullName> 类构造函数将导致产生以下 URI：  
  
 `http://www.microsoft.com/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 可以将此默认行为修改为不取消转义将 schemeSettings 配置选项用于特定方案的百分号编码的路径分隔符。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 以下代码示例示出由 <xref:System.Uri> 类使用的配置，其清除所有架构设置，然后对 http 架构非转义的百分比编码的路径分隔符添加支持。  
  
```  
<configuration>  
  <uri>  
    <schemeSettings>  
      <clear/>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Configuration.SchemeSettingElement?displayProperty=fullName>   
 <xref:System.Configuration.SchemeSettingElementCollection?displayProperty=fullName>   
 <xref:System.Configuration.UriSection?displayProperty=fullName>   
 <xref:System.Configuration.UriSection.SchemeSettings%2A?displayProperty=fullName>   
 <xref:System.GenericUriParserOptions?displayProperty=fullName>   
 <xref:System.Uri?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)