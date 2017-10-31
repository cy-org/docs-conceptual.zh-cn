---
title: "在 Windows 服务应用程序中承载 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4199998-27f3-4dd9-aee4-0a4addfa9f24
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 在 Windows 服务应用程序中承载
Windows 服务（以前称为 Windows NT 服务）提供了一种尤其适合于下面这样的应用程序的进程模型：必须在长时间运行的可执行程序中生存，并且不显示任何形式的用户界面。  Windows 服务应用程序的进程生存期由服务控制管理器 \(SCM\) 管理，您可以通过该管理器启动、停止和暂停 Windows 服务应用程序。  可以将 Windows 服务进程配置为在计算机启动时自动启动，使其成为“始终运行的”应用程序的合适的承载环境。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] Windows 服务应用程序的更多信息，请参见 [Windows 服务应用程序](http://go.microsoft.com/fwlink/?LinkId=89450)（可能为英文网页）。  
  
 承载长时间运行的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务的应用程序具有许多和 Windows 服务一样的特性。  具体而言，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务是长时间运行的服务器可执行程序，并且不与用户直接交互，因此也不实现任何形式的用户界面。  因此，在 Windows 服务应用程序内承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务是一个用于生成可靠的、长时间运行的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序的可行方案。  
  
 通常，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 开发人员必须决定是在 Windows 服务应用程序内、Internet 信息服务 \(IIS\) 内还是在 Windows 进程激活服务 \(WAS\) 宿主环境中承载他们的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序。  在下列条件下，应考虑使用 Windows 服务应用程序：  
  
-   应用程序要求显式激活。  例如，在服务器启动时应用程序必须自动启动（而不是动态启动以响应第一个传入消息）的条件下，应使用 Windows 服务。  
  
-   承载应用程序的进程必须在启动后保持运行状态。  Windows 服务进程一旦启动将一直保持运行状态，直到服务器管理员使用服务控制管理器显式关闭该进程。  在 IIS 或 WAS 中承载的应用程序可能会动态地启动和停止，以便最佳地使用系统资源。  需要显式控制其宿主进程的生存期的应用程序应使用 Windows 服务而非 IIS 或 WAS。  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务必须在 Windows Server 2003 上运行并且必须使用 HTTP 之外的传输。  在 Windows Server 2003 上，[!INCLUDE[iis601](../../../../includes/iis601-md.md)] 宿主环境限制为仅可进行 HTTP 通信。  Windows 服务应用程序不受此限制的约束，可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持的任何传输协议，包括 net.tcp、net.pipe 和 net.msmq。  
  
### 在 Windows 服务应用程序内承载 WCF  
  
1.  创建 Windows 服务应用程序。  可以使用 <xref:System.ServiceProcess> 命名空间中的类以托管代码的形式编写 Windows 服务应用程序。  此应用程序必须包含一个继承自 <xref:System.ServiceProcess.ServiceBase> 的类。  
  
2.  将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的生存期链接到 Windows 服务应用程序的生存期。  通常，人们希望 Windows 服务应用程序中承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务能够在宿主服务启动时变为活动状态，而在宿主服务停止时停止对消息的侦听，并在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务遇到错误时关闭宿主进程。  这可以通过以下操作实现：  
  
    -   重写 [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 以打开一个或多个 <xref:System.ServiceModel.ServiceHost> 实例。  一个 Windows 服务应用程序可以承载多个作为一个组同时启动和停止的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  
  
    -   重写 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 以在 <xref:System.ServiceModel.ServiceHost> 任何运行的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务上调用 <xref:System.ServiceModel.Channels.CommunicationObject.Closed>，这些服务在 [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 过程中启动。  
  
    -   订阅 <xref:System.ServiceModel.ServiceHost> 的 <xref:System.ServiceModel.Channels.CommunicationObject.Faulted> 事件，并使用 <xref:System.ServiceProcess.ServiceController> 类以在出现错误时关闭 Windows 服务应用程序。  
  
     部署和管理承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的 Windows 服务应用程序的方式与不使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 Windows 服务应用程序的一样。  
  
## 请参阅  
 <xref:System.ServiceProcess>   
 [演练：在组件设计器中创建 Windows 服务应用程序 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=94875)   
 [如何：在托管 Windows 服务中承载 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)   
 [Windows 服务主机](../../../../docs/framework/wcf/samples/windows-service-host.md)   
 [服务应用程序编程体系结构 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=94876)   
 [Windows Server App Fabric 承载功能 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=201276)