---
title: "WCF 和国际化域名 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8a3e10a-8bc2-4a78-8d86-a562ba6e65fa
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# WCF 和国际化域名
添加了允许使用带有国际化域名 \(IDN\) 的 WCF 服务的支持。  国际化域名称是包含非 ASCII 字符的域名。  这种支持包括能够承载具有 IDN 名称的 WCF 服务以及 WCF 客户端，以便与具有 IDN 名称的 Web 服务进行对话。  
  
## System.Uri 和 IDN  
 <xref:System.Uri> 具有两个属性：<xref:System.Uri.Host%2A> 和 <xref:System.Uri.DnsSafeHost%2A>。  根据 IDN 配置设置，这些属性包含 Unicode 或 Punycode 值。  
  
 使用下面的 XML 在应用程序的配置文件中启用 IDN  
  
```  
<configuration>  
  <uri>  
    <idn enabled="All/AllExceptIntranet/None" />  
  </uri>  
</configuration>  
  
```  
  
 \<idn\> 元素包含可设置为下列值之一的已启用属性：  
  
1.  “None”  
  
2.  “AllExceptIntranet”  
  
3.  “All”  
  
 在 IDN 设置设为“None”时，Uri.Host 或 Uri.DnsSafeHost 不会执行任何转换。  在 IDN 设置设为“All”时，uri.Host 保留 Unicode 并且 uri.DnsSafeHost 转换为 Punycode。  在 IDN 设置设为“AllExceptIntranet”时，uri.DnsSafeHost 转换为 Punycode 以便用于 Internet 地址，并且保留 Unicode 以便用于 Intranet 地址。  此设置对于正确的 DNS 名称解析十分重要。  请注意，无需为 Windows 8 和更新版本配置此设置。  
  
> [!WARNING]
>  您应该永远不会使用 Punycode 对地址进行硬代码。  WCF 将会基于您应用的配置设置为您转换它。  
  
> [!WARNING]
>  将 Unicode 字符添加到 applicationHost.exe.config 时，使用 UTF\-8 编码保存文件。  
  
## 请参阅  
 [System.Uri](http://msdn.microsoft.com/library/system.uri.aspx)