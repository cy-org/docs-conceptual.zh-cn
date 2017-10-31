---
title: "如何：为数据服务请求（WCF 数据服务）指定客户端凭据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF 数据服务, 自定义请求"
ms.assetid: 1632f9af-e45f-4363-9222-03823daa8e28
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：为数据服务请求（WCF 数据服务）指定客户端凭据
默认情况下，客户端库在向 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务发送请求时不提供凭据。  但是，可以通过为 <xref:System.Data.Services.Client.DataServiceContext> 的 <xref:System.Data.Services.Client.DataServiceContext.Credentials%2A> 属性提供 <xref:System.Net.NetworkCredential> 以指定发送凭据，对发送到数据服务的请求进行身份验证。  有关详细信息，请参阅[WCF 数据服务的安全](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)。  本主题中的示例演示如何显式提供 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端从数据服务请求数据时使用的凭据。  
  
 本主题中的示例使用罗斯文示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  此外，还可以使用 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 网站上发布的公共 [Northwind 示例数据服务](http://go.microsoft.com/fwlink/?LinkId=187426)（可能为英文网页）；该示例数据服务是只读的，当尝试保存更改时会返回错误。  [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 网站上的示例数据服务允许进行匿名身份验证。  
  
## 示例  
 以下示例来自 Windows Presentation Framework 应用程序的可扩展应用程序标记语言 \(XAML\) 主页文件的代码隐藏页。  该示例显示了一个 `LoginWindow` 实例，用于收集用户的身份验证凭据，然后在向数据服务发出请求时使用了这些凭据。  
  
  
  
## 示例  
 以下 XAML 定义了 WPF 应用程序的主页。  
  
  
  
## 示例  
 以下示例来自窗口的代码隐藏页，该窗口用于在向数据服务发出请求时收集用户的身份验证凭据。  
  
  
  
## 示例  
 以下 XAML 定义了 WPF 应用程序的登录。  
  
  
  
## .NET Framework 安全性  
 本主题中的示例适用以下安全注意事项：  
  
-   为验证此示例中提供的凭据是否能够正常工作，罗斯文数据服务必须使用一种非匿名访问的身份验证方案。  否则，承载数据服务的网站将不会请求凭据。  
  
-   用户凭据应仅在执行过程中请求并且不应缓存。  必须始终安全地存储凭据。  
  
-   使用基本和摘要式身份验证发送的数据不会加密，因此攻击者会看到数据。  此外，基本身份验证凭据（用户名和密码）是以明文形式发送的，会被截取。  
  
 有关详细信息，请参阅[WCF 数据服务的安全](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)。  
  
## 请参阅  
 [WCF 数据服务的安全](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)   
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)