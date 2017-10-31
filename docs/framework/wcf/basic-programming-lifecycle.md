---
title: "基本编程生命周期 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "服务创建 [WCF]"
ms.assetid: 7cf21bfe-23bd-46aa-8033-609f851dbf76
caps.latest.revision: 36
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 36
---
# 基本编程生命周期
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 可让应用程序通报它们是在同一台计算机上、分布在 Internet 上还是在不同的应用程序平台上。本主题概述了生成 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序所需的任务。有关可运行的示例应用程序，请参见[入门教程](../../../docs/framework/wcf/getting-started-tutorial.md)。  
  
## 基本任务  
 要执行的基本任务依次为：  
  
1.  定义服务协定。服务协定指定服务的签名、服务交换的数据和其他协定要求的数据。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][设计服务协定](../../../docs/framework/wcf/designing-service-contracts.md).  
  
2.  实现协定。若要实现服务协定，请创建实现协定的类并指定运行时应具有的自定义行为。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][实现服务协定](../../../docs/framework/wcf/implementing-service-contracts.md).  
  
3.  通过指定终结点和其他行为信息来配置服务。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][正在配置服务](../../../docs/framework/wcf/configuring-services.md).  
  
4.  承载服务。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][承载服务](../../../docs/framework/wcf/hosting-services.md).  
  
5.  生成客户端应用程序。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][生成客户端](../../../docs/framework/wcf/building-clients.md).  
  
 尽管本节中的主题遵循此顺序，但是一些方案并不会从头开始。例如，如果想要为预先存在的服务生成客户端，则从步骤 5 开始。或者，如果您是在生成其他人要使用的服务，则可以跳过步骤 5。  
  
 在熟悉服务协定的开发之后，还可以阅读[扩展性介绍](../../../docs/framework/wcf/introduction-to-extensibility.md)。如果服务出现问题，可参考 [WCF 疑难解答快速入门](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md)以查看其他人是否有相同或相似的问题。  
  
## 请参阅  
 [实现服务协定](../../../docs/framework/wcf/implementing-service-contracts.md)