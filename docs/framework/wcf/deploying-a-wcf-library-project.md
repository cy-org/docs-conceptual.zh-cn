---
title: "部署 WCF 库项目 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9f9222fe-d358-443c-9a49-12c5498e35e7
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 部署 WCF 库项目
本主题介绍如何部署 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务库项目。  
  
## 部署 WCF 服务库  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库是一个动态链接库 \(DLL\)。因此，它不能自己运行。必须将其部署到宿主环境中。有关此过程的更多信息，请参见[承载和使用 WCF 服务](http://go.microsoft.com/fwlink/?LinkId=99932)（可能为英文网页）。  
  
 可以像部署任何其他 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务一样部署 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库。但是，请注意，[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 不支持配置为 Dll。<xref:System.Configuration> 支持每个应用程序域的一个配置文件。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库项目通过在开发期间为库提供 App.config 文件来减少此限制。但在部署之后不能识别 App.config 文件。  
  
 必须将配置代码移动到宿主环境所识别的配置文件中。对于自承载，您应将 App.config 文件的内容复制到宿主可执行文件的 App.config 文件中。如果使用 IIS 承载服务，则应将 App.config 文件的内容复制到虚拟目录的 Web.config 文件中。