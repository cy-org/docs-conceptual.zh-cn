---
title: "WCF 所要求的操作系统资源 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cdd9a331-53fe-4e0d-bdfe-782264aec5c9
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# WCF 所要求的操作系统资源
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 的正常运行依赖于操作系统提供的几种资源。  下表列出了这些资源。  
  
|资源|描述|  
|--------|--------|  
|Microsoft 分布式事务协调器 \(MSDTC\)|支持 OleTx 事务所必需。|  
|Internet 信息服务 \(IIS\)|如果希望使用 IIS 来承载应用程序，则是必需的。|  
|Windows 进程激活服务 \(WAS\)|如果希望使用 WAS 来承载应用程序，则是必需的。|  
  
## 请参阅  
 [系统要求](../../../docs/framework/wcf/wcf-system-requirements.md)