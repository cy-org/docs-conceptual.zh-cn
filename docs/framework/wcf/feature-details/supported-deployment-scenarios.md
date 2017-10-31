---
title: "支持的部署方案 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3399f208-3504-4c70-a22e-a7c02a8b94a6
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# 支持的部署方案
可在部分受信任的应用程序中使用的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 功能子集旨在满足使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的某些（而非全部）方案的要求。 在服务器上，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可满足 Internet 规模的共享宿主提供程序的要求，出于安全原因，这些提供程序在 [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] 中以“中等信任”权限集运行第三方应用程序。 在客户端上，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 部分信任支持旨在满足某些部署技术（例如 [ClickOnce Deployment](http://go.microsoft.com/fwlink/?LinkId=83712)（ClickOnce 部署）或 [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] 的 XAML 浏览器应用程序技术）的要求，通过这些部署技术可以从不受信任的网站对桌面应用程序进行无缝和安全地部署。  
  
## 最低权限要求  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在通过以下任一标准命名权限集运行的应用程序中支持一个功能子集：  
  
-   “中等信任”权限  
  
-   “Internet 区域”权限  
  
 尝试在部分受信任的应用程序利用具有更多限制的权限来使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可能在运行时导致安全异常。  
  
 有关这些权限集支持的功能的详细信息，请参阅[部分信任功能兼容性](../../../../docs/framework/wcf/feature-details/partial-trust-feature-compatibility.md)。  
  
## 服务器上的部分信任  
 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 应用程序宿主服务的许多商业提供程序要求在其服务器上的应用程序以 [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] 中等信任权限集来运行。 只要 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务使用具有传输级安全的 <xref:System.ServiceModel.BasicHttpBinding>、<xref:System.ServiceModel.WebHttpBinding> 或 <xref:System.ServiceModel.WsHttpBinding>，就可以在这些环境中运行。  
  
 在中等信任宿主环境中运行的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务还可以充当中间层服务，将消息发送到其他服务器以响应客户端请求。 如果宿主环境已授予应用程序适当的 <xref:System.Net.WebPermission> 以向所需服务器发出出站请求，则支持服务器上的中间层方案。  
  
 除了使用支持的 SOAP 绑定之一的 SOAP 消息传递之外，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 还支持 <xref:System.ServiceModel.WebHttpBinding>，用于在部分受信任的应用程序中生成 Web 样式服务。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 [WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)、[WCF 联合](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)和 [AJAX 集成和 JSON 支持](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)功能在部分信任中均受支持。  
  
 工作流服务需要完全信任权限并且不能在部分受信任的应用程序中使用。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [How to: Use Medium Trust in ASP.NET 2.0](http://go.microsoft.com/fwlink/?LinkId=84603)（如何：在 ASP.NET 2.0 中使用中等信任）。  
  
## 客户端上的部分信任  
 在从不受信任的 Internet 网站上下载和运行代码时必须采用某些安全预防措施。[ClickOnce Deployment](http://go.microsoft.com/fwlink/?LinkId=83712)（ClickOnce 部署）和 [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] 的 XAML 浏览器应用程序 \(XBAP\) 技术都可以使用部分信任以对不受信任的代码授予受限权限（Internet 区域）。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可用于从通过 [ClickOnce Deployment](http://go.microsoft.com/fwlink/?LinkId=83712)（ClickOnce 部署）或 XBAP 技术部署的部分受信任的应用程序中与远程服务器进行通信。 Internet 区域权限集包括发起主机的 <xref:System.Net.WebPermission>，此权限允许这些程序使用任何支持的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 绑定（[部分信任功能兼容性](../../../../docs/framework/wcf/feature-details/partial-trust-feature-compatibility.md)中进行了介绍）来与其源服务器进行通信。  
  
## 请参阅  
 [代码访问安全性](http://go.microsoft.com/fwlink/?LinkId=83717)   
 [Windows Presentation Foundation 浏览器托管的应用程序概述](http://go.microsoft.com/fwlink/?LinkId=98397)   
 [部分信任](../../../../docs/framework/wcf/feature-details/partial-trust.md)   
 [ASP.Net 中等信任](http://go.microsoft.com/fwlink/?LinkId=69328)