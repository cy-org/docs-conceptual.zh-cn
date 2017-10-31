---
title: "承载排队应用程序的 Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7a539fa-e442-4c08-a7f1-17b7f5a03e88
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# 承载排队应用程序的 Web
Windows 进程激活服务 \(WAS\) 管理辅助进程的激活和生存期，该辅助进程包含承载 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务的应用程序。  WAS 进程模型通过移除对 HTTP 的依赖性使 HTTP 服务器的 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 进程模型通用化。  这就使 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可以在宿主环境中同时使用 HTTP 和非 HTTP 协议（如 net.msmq 和 msmq.formatname），该宿主环境支持基于消息的激活以及在给定计算机上提供承载大量应用程序的能力。  
  
 WAS 中包含一项消息队列 \(MSMQ\) 激活服务，当有一条或多条消息放入某排队的应用程序所使用的某个队列时，该服务将激活该应用程序。  MSMQ 激活服务是默认情况下自动启动的 NT 服务。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] WAS 及其优点的更多信息，请参见[在 Windows 进程激活服务中承载](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] MSMQ 的更多信息，请参见[队列概述](../../../../docs/framework/wcf/feature-details/queues-overview.md)  
  
## WAS 中的队列寻址  
 WAS 应用程序具有统一资源标识符 \(URI\) 地址。  应用程序地址有两部分：基本 URI 前缀和应用程序特定的相关地址（路径）。  这两部分连接在一起时可提供应用程序的外部地址。  基本 URI 前缀从网站绑定进行构造并且适用于网站上的所有应用程序，例如，“net.msmq:\/\/localhost”、“msmq.formatname:\/\/localhost”或“net.tcp:\/\/localhost”。  然后通过使用应用程序特定的路径片段（如“\/applicationOne”）来构造应用程序地址并将其追加到基本 URI 前缀，以形成完整的应用程序 URI，例如“net.msmq:\/\/localhost\/applicationOne”。  
  
 MSMQ 激活服务使用应用程序 URI 来匹配 MSMQ 激活服务必须监视其消息的队列。  MSMQ 激活服务启动时，它将枚举配置为从其中接收消息的计算机上所有的公共队列和专用队列，以及监视消息的公共队列和专用队列。  每隔 10 分钟，MSMQ 激活服务就刷新一次要监视的队列列表。  在队列中找到消息时，激活服务将队列名称与 net.msmq 绑定的最长匹配应用程序 URI 进行匹配，并激活该应用程序。  
  
> [!NOTE]
>  被激活的应用程序必须与队列名称的前缀匹配（最长的匹配）。  
  
 例如，队列名称为：msmqWebHost\/orderProcessing\/service.svc。  如果应用程序 1 的下面有一个带有 service.svc 的虚拟目录 \/msmqWebHost\/orderProcessing，应用程序 2 的下面有一个带有 orderProcessing.svc 的虚拟目录 \/msmqWebHost，则将激活应用程序 1。  如果应用程序 1 已删除，则将激活应用程序 2。  
  
> [!NOTE]
>  创建队列后，在 MSMQ 激活服务刷新队列列表（自创建该队列时起最多 10 分钟）之前，发送到该队列的任何消息都不会激活应用程序。  重新启动激活服务也会刷新队列列表。  
  
### 专用队列和公共队列对寻址的影响  
 MSMQ 激活服务并不区分专用队列和公共队列监视。  因此，您不能拥有名称相同的公共队列和专用队列。  如果有，则 Web 承载的应用程序可能被激活，从这两个队列之一中进行读取。  
  
### 用于激活的队列配置  
 MSMQ 激活服务将作为 NETWORK SERVICE 运行。  这是监视要激活应用程序的队列的服务。  由于它将从队列激活应用程序，因此该队列必须提供 NETWORK SERVICE 访问权限以查看其访问控制列表 \(ACL\) 中的消息。  
  
### 病毒消息  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的病毒消息处理由通道执行，通道不仅检测中毒的消息，还会根据用户配置选择处理。  因此，队列中仅有一条消息。  Web 承载的应用程序可连续多次中止并将该消息移到重试队列中。  在重试周期延迟确定的点，消息从重试队列中移到主队列以便进行重试。  但是这要求排队通道应是活动的。  如果 WAS 回收了该应用程序，则在另一条消息到达主队列以激活排队应用程序之前，此消息仍保留在重试队列中。  本例中的解决方法就是手动将消息从重试队列移回主队列，以便重新激活应用程序。  
  
### 子队列和系统队列注意事项  
 不能基于系统队列（如系统级死信队列）或子队列（如病毒子队列）中的消息激活 WAS 承载的应用程序。  这是此版本产品的一个限制。  
  
## 请参阅  
 [病毒消息处理](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)   
 [服务终结点和队列寻址](../../../../docs/framework/wcf/feature-details/service-endpoints-and-queue-addressing.md)