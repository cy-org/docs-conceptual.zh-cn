---
title: "快速入门（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "HTML"
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "WCF 数据服务, 快速入门示例"
  - "WCF 数据服务, 实体数据模型 (EDM) 服务"
ms.assetid: 7b18ca1e-d4d6-4c7a-afb9-ce3cebb98a8d
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 快速入门（WCF 数据服务）
本快速入门通过支持 [入门](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md) 中的各个主题的一系列任务来帮助你熟悉 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 和 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]。  
  
## 学习内容  
 本快速入门中的第一项任务介绍如何创建数据服务以公开罗斯文示例数据库中的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源。 在后面的主题中，您将使用 Web 浏览器访问 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源，还将创建一个 [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)] 客户端应用程序，它通过客户端库使用 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源。  
  
## 先决条件  
 为了完成本快速入门，必须安装以下组件：  
  
-   [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]。  
  
-   [!INCLUDE[msCoName](../../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 的一个实例。 这包含 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 的默认安装中包括的 SQL Server Express。  
  
-   Northwind 示例数据库。 若要下载此示例数据库，请访问 [SQL Server 的示例数据库](http://go.microsoft.com/fwlink/?linkid=24758)下载页。  
  
## WCF 数据服务快速入门任务  
 [创建数据服务](../../../../docs/framework/data/wcf/creating-the-data-service.md)  
 定义 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序，定义数据模型，创建数据服务，并启用对资源的访问。  
  
 [从 Web 浏览器访问服务](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)  
 通过 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 启动服务，并通过 Web 浏览器向公开的源提交 HTTP GET 请求以访问该服务。  
  
 [创建 .NET Framework 客户端应用程序](../../../../docs/framework/data/wcf/creating-the-dotnet-client-application-wcf-data-services-quickstart.md)  
 创建一个 [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] 客户端应用程序以使用 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源，将数据绑定到 Windows 控件，在绑定控件中更改数据，然后将更改发送回数据服务。  
  
> [!NOTE]
>  已完成版本的快速入门中的项目文件可从 [WCF 数据服务文档示例](http://go.microsoft.com/fwlink/?LinkId=179994) 网页下载。  
  
## 后续步骤  
 [启动快速入门](../../../../docs/framework/data/wcf/creating-the-data-service.md)。  
  
## 请参阅  
 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)