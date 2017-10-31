---
title: "在托管应用程序中承载 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: af70132d-e9e1-4f32-b20f-f0014629758a
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 在托管应用程序中承载
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务可以承载于任何 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 应用程序中。 自承载服务是最灵活的宿主选项，因为此服务部署所需要的基础结构最少。 但是，此服务也是最不可靠的宿主选项，因为托管应用程序未提供 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中其他宿主选项（如 Internet 信息服务 \(IIS\) 和 Windows 服务）的高级宿主和管理功能。  
  
 若要创建自承载服务，请创建并打开 <xref:System.ServiceModel.ServiceHost> 的实例以启动侦听消息的服务。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [如何：在托管应用程序中承载 WCF 服务](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md).  
  
 有关如何定义协定、实现协定以及在托管应用程序内托管服务的完整示例，请参阅[入门教程](../../../../docs/framework/wcf/getting-started-tutorial.md)和[自承载](../../../../docs/framework/wcf/samples/self-host.md)。  
  
 以下各部分描述了使用此宿主选项的常见情况。  
  
## 控制台应用程序  
 自承载支持的常见方案是在控制台应用程序内部运行的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。 在控制台应用程序内部承载一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务通常在服务的开发阶段非常有用。 这使服务变得容易调试，从中跟踪信息以查明应用程序内发生的情况变得更加方便，以及通过将其复制到新的位置进行来回移动变得更加轻松。  
  
## 胖客户端应用程序  
 自承载支持的其他常见方案是胖客户端应用程序，如基于 [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)] 或 Windows 窗体 \(WinForms\) 的应用程序。 此宿主选项还使丰富客户端应用程序（如 [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] 和 WinForms 应用程序）与外部世界的通信变得很容易。 例如，一个将 [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] 用于其用户界面并作为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务主机的对等协作客户端，允许其他客户端连接到它并共享信息。  
  
## 请参阅  
 [承载服务](../../../../docs/framework/wcf/hosting-services.md)   
 [入门教程](../../../../docs/framework/wcf/getting-started-tutorial.md)